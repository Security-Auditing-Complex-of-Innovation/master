General consensus is that more or less all of the vulnerabilities found during our scanning of both the inside and outside address spaces of the 1:1 NAT could have been fixed by running software updates on the relevant servers.
Now, the reason for this is that there simply was no updates available in the RGCE mirrors, hence we've decided to skip the low hanging fruits this scenario proposed and instead we attempted to come up with some less obvious findings and discuss few of the critical flaws found in more detail, that being said, in more general level concerning the given well known vulnerabilities.

## Port scanning and the oddities detected

The scan in general didn't show any errors, like critical vulnerabilities, but there is a possible configuration error in form of BGP tcp/179 being reachable from our Nessus scanner. Danger in this configuration is that BGP port is a sign of possibly lacking control plane protections on the ISP router. Possible exploitation vectors include things such as sending RST packet from falsified source address and general overloading of the BGP process on the listening party. Net effect of this is that the would-be BGP peering might be prone to denial of service, given that there is no peerings configured BGP tcp/179 should not be open to begin with. Assuming that the open BGP port is for future use cases we'd like to propose the following mitigation methods:

1) Filter inbound packets based on TTL value - this could be done on both ends of the BGP peering
2) Make sure that the uRPF filters are utilized on both the ISP network in general and in the customer peerings 

### Issues with the port scanning

We attempted to port scan the whole subnet using various nmap switches. But during our testing we witnessed some strange behaviour on the ldil.de firewall. Next is a brief description of the open ports detected and the aforementioned behaviour of interest.
Nevertheless, we got some results in overall, after combining the results achieved from the Nessus scan and partial results of NMAP. First we will depict the results achieved from the scanning executed from outside the firewall.
The first IP found was 79.99.192.1. According to the documentation, this is the RGCE ISP. See the above note concerning the BGP configuration. 
The next IP found was 79.99.193.10. According to Nessus this IP address belongs to extranet.ldil.de, the Extranet service. Although this server likely hosts http services, the top 1000 ports were all displayed as filtered.
This was likely due to feature of the paloalto firewall that we'll discuss later on this report.

The IP 79.99.193.20 belongs to the store service. All top 1000 service ports were filtered according to nmap and Nessus scans. This makes no sense, as the store should definitely serve publicly from ports 80 and 443.
This, similarly to the previous finding, will be discussed in further detail later on.

Apparently the PaloAlto firewall starts to shun source addresses that it deems as sources of port scanning. This is all good as such but it provides interesting vector for denial of service as follows. An attacker could forge the source address of the connection so that the source IP address could come from one or more of the critical interest groups. At least some form of whitelisting should take place as uRPF filters are not deployed fully in the Internet and even if the first next-hop ISP did utilize uRPF the whole of Internet does not. Whitelisting of source addresses would mitigate the DOS vector in a simple manner, except that the web store should be reachable from everywhere, hence the source address filter is not enough on its own. Whitelisting the tcp/80 and tcp/443 for web store would mitigate this to some extent. Yet, whitelisting would open the door for flooding the firewall state table for the givenwhite listed ports. Hence the recommendation would be to consider using stateless filters in ISP routers for the mandatory tcp/80 and tcp/443 and do the specific filtering in paloalto for others non "access from anywhere" services utilizing whitelisting.

### Scans from inside

First interesting finding was 10.10.10.7. What makes this address so compelling is that there was no mention of this address in the documention eg. excel sheet. This on its own could be a severe anomaly, especially as we failed to login via ssh using the passwords and usernames available. To increase the importance of this finding was the tftp-server running on the host. We tested this by uploading some files. This means that not only was the host not documented, but it also had write access made available via TFTP. This could be exploited in terms of denial of service by filling the disk on the receiving end, obviously depending on the TFTP configuration. Uncomented ip addresses might be an indication of problems implementing change management and other administrative procedures. Two other non-documented addresses where found, namely Kali and Nessus - obviously these where not present in the time when the documentation was written but these could still be seen as worthwhile indicators of documentation lagging behind.

### General findings

As stated before we will not got over each and every one of the findings - since these would have been mitigated via software updates, and due to the fact that hardening was likeli not applied to each host to begin with- instead we'll focus on few of the key findings and the exploit method behind. Nevertheless, next is a list of few of the more severe findings followed by the key exploits of interest.

Extranet host had ssh open from everywhere from the local iptables firewall. Eg. input policy was set to ACCEPT.
Likeli this host had no indepth ssh hardening done.

Magento host had basic authentication without encryption and phpmyadmin 

SMTP host had plaintext authentication supported. Possible source of leaking user accounts.

We opted to discuss the following vulnerabilities in more detail:

#### Shellshock

####¤ General overview of shellshock and its availability within the LDIL

shellshock, also known as bashdoor is a security vulnerability found in the bourne again shell (bash) -type of shell.
Shellshock was seen first time in september 2014, yet this vulnerability appears to be present in LDIL environment, likely due to software upgrades being unavailable, since shellshock is relatively trivial to patch simply by upgrading the bash shell to newer, less vulnerable version.

During our scanning shellshock vulnerability was detected in the following addresses:

10.10.10.8 ns2.ldil.de
10.10.10.10 extranet.ldil.de
10.10.10.20 files.ldil.de
10.10.10.40 helpdesk.ldil.de

It should be noted that these where found during the scanning from the *inside* of the network.
These vulnerabilities where not detected during the scanning from outside - this could be due to various factors such as:

* The dynamic manner how the PaloAlto firewall responded to port scanning by blocking the source address during scanning
* Possibly due to packet filtering taking place as expected

Nevertheless, shellshock opens interesting opportunities for exploitation assuming some means to access the aforementioned hosts inside the packet filtering perimeter. 
Next we'll discuss the general methodology behind shellshock and some means how it might be exploited within LDIL.
Given that the fix is trivial software upgrade it was not deemed necessary to discuss the details of the remedy method.

####¤ How shellshock works - what makes it interesting?

As previously stated, shellshock is vulnerability in the bash shell. More indepth explanation is that bash untintentionally executes directives when commands are chained to the very end of the function definitions that in turn are stored values within the system environment variables.
What makes shellshock so nasty is that the way it exploits the bash function export -feature to a net effect of providing user access to functionality that is not supposed to be available to the user executing the bash shell.
This happens since each instance of bash scans the environment variable list for scripts, and assembles these scripts into a statement that defines the script within the new instance and finally executes the command. Bash has no means to verify the origin or validity of these script definitions. This leads to a scenario where attacker can execute commands on the system or abuse other bugs that might exist in bash.
Given that the mentioned functionality might sound solely locally exploitable vulnerability, unfortunately this is not the case as various pieces of remotely reachable software - such as web servers - might utilize bash to execute functions such as system(). This means that shellshock is not only locally exploitable.

As a proof of this in the first phases shellshock announcement it was actively exploited by DoS -practitioners, mostly to build botnets utilized in DDoS attacks.

##### Weak cryptographic ciphers

This is a general discussion concerning the known-weak cryptographic ciphers found from LDIL.de -environment.

We will also discuss few of the known vulnerabilities related to weak ciphers, namely arcfour (eg. alleged rc4), cbc and mac algorithms. 

##### How these effect ldil.de?

By using weak ciphers it is possible that some or all parts of the encrypted message could be made readable by offender. This is especially critical for administrative traffic, since administrative infrastructure can be seen as one step more secret than the production environment being administrated, namely ST4 environment could be administrated from ST3 administration environment.           

Since it is possible to use only computationally secure algorithms it is good idea to make sure that the algorithms used are not too quick, cheap or trivial to reverse by means of brute force.
 
Weak algorithms are especially critical for web shop applications that when exploited can have severe complications in terms of loss of reputation, loss of client data and loss of business.


