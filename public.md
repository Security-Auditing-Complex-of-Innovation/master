# DMZ

## Audit activities (4.1)

Premilinary scanning of the public address space and 1:1 NAT inside network was performed using Nessus vulnerability scanner and nmap port scanner. Two aforementioned tools were used from both inside and outside of the perimeter firewall. First order of business was running nmap and Nessus was used to both confirm the nmap findings and to scan for higher level vulnerabilities. Reports produced by the automated scanners were analyzed manually to find the most relevant issues that were deemed worthy of escalation. Masses of bulk vulnerabilities that were found where intentionally left out as they could have been trivially patched assuming patches where available in RGCE. These are still reported in the attachements.

Hence, we selected two of the more critical and subject-wise interesting vulnerabilities: shellshock and weak encryption mechanisms. Both of these were discussed in more detail from the ldil.de perspective with PCI DSS angle. No detailed recommendations for fixes were given as these issues can be trivially mitigated from the technical point of view. 

## Summary of findings within the DMZ (5)

General consensus is that more or less all of the vulnerabilities found during our scanning of both the inside and outside address spaces of the 1:1 NAT could have been fixed by running software updates on the relevant servers.
Now, the reason for this is that there simply was no updates available in the RGCE mirrors, hence we've decided to skip the low hanging fruits this scenario proposed and instead we attempted to come up with some less obvious findings and discuss few of the critical flaws found in more detail, that being said, in more general level concerning the given well known vulnerabilities.

## Issues with the port scanning (5)

We attempted to port scan the whole subnet using various NMAP switches. But during our testing we witnessed some strange behaviour on the ldil.de firewall. Next is a brief description of the open ports detected and the aforementioned behaviour of interest. Nevertheless, we got some results in overall, after combining the results achieved from the Nessus scan and partial results of NMAP scans. First we will depict the results achieved from the scanning executed from outside the firewall.

## Vulnerability findings found from outside the perimeter firewall (7.6)

### BGP port open

**Synopsis**: See the aforementioned paragraph concerning the BGP configuration.

**Vulnerable Target**: 79.99.192.1. According to the documentation, this is the RGCE ISP.

**Vulnerability Explanation**: There is a possible configuration error in form of BGP tcp/179 being reachable from our Nessus scanner. Danger in this configuration is that BGP port is a sign of possibly lacking control plane protections on the ISP router. Possible exploitation vectors include things such as sending RST packet from falsified source address and general overloading of the BGP process on the listening party. Net effect of this is that the would-be BGP peering might be prone to denial of service attacks, given that there is no peerings configured, the BGP tcp/179 should not be open to begin with. Hence, as an exception to the previously mentioned lack of recommended fixes we'd like to point out the following: Assuming that the open BGP port is for future use cases we would like to propose the following mitigation methods.

1) Filter inbound packets based on TTL value - this could be done on both ends of the BGP peering
2) Make sure that the uRPF filters are utilized on both the ISP network in general and in the customer peerings 


### Service port closed for extranet service

**Synopsis**: HTTP(S) service port closed for a likely HTTP(S) server

**Vulnerable Target**: 79.99.193.10. According to Nessus this IP address belongs to extranet.ldil.de, the Extranet service.

**Vulnerability Explanation**: Although this server likely hosts HTTP(S) services, the top 1000 ports were all displayed as filtered. This was likely due to feature of the PaloAlto firewall that we'll discuss later on this report.

### Service port closed

**Synopsis**: HTTP(S) service port closed for a HTTP(S) server

**Vulnerable Target**: 79.99.193.20 belongs to the store service.

**Vulnerability Explanation**: All top 1000 service ports were filtered according to the NMAP and Nessus scans. This doesn't sound right, as the store should definitely serve publicly from ports 80 and 443. This, similarly to the previous finding, will be discussed in further detail later on.

### Remotely triggerable filtering of ports by the firewall

**Synopsis**: Traffic rejection treshold prone for remote triggering

**Vulnerable Target**: 79.99.193.1, PaloAlto firewall

**Vulnerability Explanation**: Apparently the PaloAlto firewall starts to shun source addresses that it deems as sources of port scanning. This is all good as such but it provides interesting vector for denial of service attacks as follows. An attacker could forge the source address of the connection so that the source IP address could come from one or more of the critical interest groups. At least some form of whitelisting should take place as uRPF filters are not deployed fully in the Internet and even if the first next-hop ISP did utilize uRPF the whole of Internet does not. Whitelisting of source addresses would mitigate the DoS vector in a simple manner, except that the web store should be reachable from everywhere, hence the source address filter is not enough on its own. Whitelisting the tcp/80 and tcp/443 for web store would mitigate this to some extent. Yet, whitelisting would open the door for flooding the firewall state table for the given whitelisted ports. Hence, the recommendation would be to consider using stateless filters in ISP routers for the mandatory tcp/80 and tcp/443 and do the specific filtering in the PaloAlto firewall for other non "access from anywhere" services utilizing whitelisting.

## Vulnerability findings found from inside the perimeter firewall (7.6)

### Introduction from DMZ scans from the inside interface
As scans executed from the outside interface were greatly affected by the behaviour of the firewall, more information about ports and services were gathered by scanning from the private network. This, nevertheless, bypasses the security provided by the firewall. On the other hand, as defence should always be multilayered and should not trust solely a single point of protection, the results can be considered as valid from the point of view of a public network, as the scans executed from therein.

### Undocumented device with services open

**Synopsis**: There are undocumented apparel in the network, with open services

**Vulnerable Targets**: 10.10.10.7, 79.99.193.251, 79.99.193.234

**Vulnerability Explanation**: First interesting finding was 10.10.10.7. What makes this address so compelling is that there was no mention of this address in the documention e.g. excel sheet. This on its own could be a severe anomaly, especially as we failed to login via SSH using the passwords and usernames available. To increase the importance of this finding was the TFTP server running on the host. We tested this by uploading some files. This means that not only was the host not documented, but it also had write access made available via TFTP. This could be exploited in terms of denial of service by filling the disk on the receiving end, obviously depending on the TFTP configuration. Uncomented IP addresses might be an indication of problems implementing change management and other administrative procedures. Two other undocumented addresses were found, namely Kali and Nessus - obviously these where not present in the time when the documentation was written but these could still be seen as worthwhile indicators of documentation lagging behind.

## General findings

As stated before, we will not go over each and every one of the findings - since these would have been mitigated via software updates, and due to the fact that hardening was likely not applied to each host to begin with, instead we'll focus on few of the key findings and the exploit method behind. Nevertheless, next is a list of few of the more severe findings followed by the key exploits of interest.

### SSH port unfiltered

**Synopsis**: SSH port open from everywhere

**Vulnerable Target**: 10.10.10.10 (extranet.ldil.de)

**Vulnerability Explanation**: Extranet host had SSH open from everywhere from the local iptables firewall. In practice, the input policy was set to ACCEPT, which thus allows SSH connections from anywhere. Likely this host had no in-depth SSH hardening done.

### Non-hardened services

**Synopsis**: Services are not hardened for restricting attack surface

**Vulnerable Target**: 10.10.10.20 (www.ldil.de)

**Vulnerability Explanation**: Magento host had several issues. To name a few: firstly basic authentication without encryption was detected, PHPMyAdmin was visible and directory browsing enabled as reported by Nessus. No authentication details should be never sent as clear text, as this would make it possible to harvest login details with simple data sniffing. PHPMyAdmin is a web frontend to administer SQL databases. This is a very powerful tool and should be absent in production servers or heavily protected by strict access limiting and other methods. The third problem brought out here is the directory browsing. This feature make it possible to for example gain valuable information about the files and directories available in the system. A good example of this could be a backup file which would make an executable file rendered as a text file providing extensive details about the system, or revealing a htaccess file to reveal the password hashes to the attacker.

### Plaintext authentication supported

**Synopsis**: Plaintext authentication for SMTP is supported

**Vulnerable Target**: 10.10.10.30 (mail.ldil.de)

**Vulnerability Explanation**: SMTP host had plaintext authentication supported. This is a possible source of leaking user accounts.It is worth mentioning that the weaknesses in configurations mentioned above on Magento, SMTP and extranet hosts represent the type where simple software update does not likely solve the problem itself. Instead, manual configuration changes are required to mitigate the errors in question.

### Shellshock

**Synopsis**: Shellshock, also known as Bashdoor, is a security vulnerability found in the Bourne Again shell (Bash).

**Vulnerable Target**: 10.10.10.8 (ns2.ldil.de), 10.10.10.10 (extranet.ldil.de), 10.10.10.20 (www.ldil.de), 10.10.10.40 (helpdesk.ldil.de)

**Vulnerability Explanation**: Shellshock, also known as Bashdoor, is a security vulnerability found in the Bourne Again shell (Bash). Shellshock was seen first time in september 2014, yet this vulnerability appears to be present in LDIL environment likely due to software upgrades being unavailable, since Shellshock is relatively trivial to patch simply by upgrading the bash shell to newer, less vulnerable version.

It should be noted that these where found during the scanning from the *inside* of the network.
These vulnerabilities were not detected during the scanning from outside - this could be due to various factors such as:

 * The dynamic manner how the PaloAlto firewall responded to port scanning by blocking the source address during scanning
 * Possibly due to packet filtering taking place as expected

Nevertheless, Shellshock opens interesting opportunities for exploitation assuming some means to access the aforementioned hosts inside the packet filtering perimeter.

Next we'll discuss the general methodology behind shellshock and some means how it might be exploited within LDIL. Given that the fix is trivial software upgrade it was not deemed necessary to discuss the details of the remedy method.

As previously stated, Shellshock is vulnerability in the Bash shell. More in-depth explanation is that Bash unintentionally executes directives when commands are chained to the very end of the function definitions that in turn are stored values within the system environment variables. What makes Shellshock so nasty is that the way it exploits the Bash function export feature to a net effect of providing user access to functionality that is not supposed to be available to the user executing the Bash shell. This happens since each instance of Bash scans the environment variable list for scripts, and assembles these scripts into a statement that defines the script within the new instance and finally executes the command. Bash has no means to verify the origin or validity of these script definitions. This leads to a scenario where attacker can execute commands on the system or abuse other bugs that might exist in Bash.

Given that the mentioned functionality might sound solely locally exploitable vulnerability, unfortunately this is not the case as various pieces of remotely reachable software - such as web servers - might utilize Bash to execute functions such as system(). This means that Shellshock is not only locally exploitable. As a proof of this in the first phases Shellshock announcement it was actively exploited by DoS practitioners, mostly to build botnets utilized in DDoS attacks.

**Business impacts of the attack vector**: This being said, ldil.de runs largely on top of web servers hosted on Linux environment when bash tends to be the default shell. This sets the ground for urgency of updating the shell since shellsock provides ground for taking out or corrupting part of the core business infrastructure, namely the web shop. This is also key element in terms of fulfilling the PCI DSS security requirements set for the platform producing the service. These are obvious fail-factors for audit.

### Weak cryptographic ciphers

**Synopsis**: This is a general discussion concerning the known weak cryptographic ciphers found from LDIL.de environment. We will also discuss few of the known vulnerabilities related to weak ciphers, namely arcfour (eg. alleged RC4), CBC and weak MAC algorithms. These weak ciphers were found from multiple hosts in the ldil.de environment, for instance the magento based web shop. This on its own is a significant business risk as ldil.de relies largely on the web shop infrastucture to work.

**Vulnerable Target**: 10.10.10.20 (www.ldil.de)

**Vulnerability Explanation**: By using weak ciphers it is possible that for example some or all parts of the encrypted message could be made readable by offender. This is especially critical for administrative traffic, since administrative infrastructure can be seen as one step more confidential than the production environment being administrated, namely restricted environment could be administrated from a secret administration environment.           

Since it is in practice possible to use only computationally secure algorithms it is a good idea to make sure that the algorithms used are not too quick, cheap or trivial to reverse without immense computing power. Thus, it is greatly discouraged to use bad ciphers which for example RC4 is with its several known flaws.

CBC (Cipher Block Chaining) used in SSH also has known vulnerabilities. By taking advantage of these vulnerabilities, an attacker might recover plaintext from the ciphertext. Thus it is strongly adviced to disable CBC from cipher sets. The last issue discussed here is the use of weak MAC algorithms. MAC (Message Authentication Code) algorithms are used to ensure integrity of the messages. Integrity issues as such don't reveal the secured data directly, but as integrity is still a basic part of security, the weaknesses should not be around on purpose. In this case for example, MD5 is used as one possible algorithm. MD5 is prone to hash collisions with very little effort, thus it is fairly trivial to falsify the message whilst keeping the MD5 sum identical to the original one.
 
Weak algorithms are especially critical in web shop applications which, when exploited, can have severe complications in terms of loss of reputation, client data and business. Several weak algorithms have for example known man-in-the-middle attack methods, which make it possible to capture the traffic by a malicious third party. Attacks like POODLE, which was identified by Nessus in several services, could be used to launch an attack of this sort.

In general, it is very important to keep all communication data properly encrypted, by using recommended crypto settings. Usually communication happens on top of a less secure media, for example the Internet, which can not be fully controlled by the administration and data protection plays a huge part in there. It should be noted that while some of the issues mentioned here could have been mitigated by updating the relevant packages - assuming those where available in RGCE to begin with - there is also need for changes in application server configuration in order for the weak ciphers to be disabled. This emphasises the importance of change management and keeping up with latest security bulletins, such as NCSA mailing list.

**Business impacts of the attach vector**:These ciphers are part of the webshop environment, but their effects can be seen in other services as well, such as SSH. SSH, being used for maintenace tasks makes it even more critical for these vulnerabilities to get patched the soonest. This makes encryption a critical audit criteria.
