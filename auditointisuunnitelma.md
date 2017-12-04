# Audit plan #
## Audit of LDIL card payment infrastructure ##
-----

## Contents ##

-----

# 1 Introduction #

LDIL is a national e-tailing company that also has one physical retail store with a POS-system. LDIL business environment consists of information systems and different network domains. Target of this evaluation is LDIL's systems and networks related to customer and payment information.


# 2 Audit target #

As described in the introduction, LDIL operates in multiple categories of the PCI DSS context. Due to the basic retail shop business the role of the LDIL mostly falls in the category of merchat, yet company's business model also includes components of payment service provider role. There are only small differences in these roles regarding the audit, but these two roles define different regional laws that should be noted:

- Payment Service Law (2010/290)
- Payment Institution Law (2010/297)

PCI DSS comprises a minimum set of requirements, which can be enhanced by regional laws and regulations. In this audit the criteria is defined only through the PCI Data Security Standard, while dependencies related to regional laws are left as a note.

## 2.1 ## 

Evaluation/Certification: Evaluation

Audit criteria: PCI DSS

Roles: Owner: President of LDIL ltd., Users: LDIL personnel and e-commerce customers

Protection level: N/A 

Timeframe of the audit: N/A

# 3 Applicability #

Parts of organization and processes that are being audited: Systems used by LDIL for managing payment card transactions and other closely related interfaces.

PCI DSS requirements apply to organizations or entities that store, process or transmit cardholder data or sensitive authentication data. LDIL is an e-commerce company that administers their own e-commerce platform and a point of sale systems at their branch store, thus making LDIL's payment system applicable to PCI DSS requirements. 

Storage of sensitive authentication data is forbidden by PCI DSS. On top of PCI DSS requirements, payment card brands can have their own instructions whether storage is permitted prior to authorization. Individual payment card brands requirements are left out the scope of this audit and focus is kept on PCI DSS requirements.

## 3.1 Scoping ##

Purpose of scoping is to determine which components of LDIL's business environment are part of cardholder data environment. Cardholder data environment comprises of LDIL's payment system components and all other connected systems.

Determining the scale of cardholder data environment is done by reviewing LDIL's provided documentation of the current business environment and security measures. Once the cardholder data environment and cardholder data flow in the payment system is identified and documented, the determined PCI DSS scope is reviewed by the LDIL before beginning the assesment (at least in real life case). 

LDIL cardholder data environment (according to LDIL documentation fig. 1, page 8):

* Magento server (e-commerce platform, payment system component)
* All other hosts in DMZ network segment (located at the same segment as Magento)
* POS Cyclos (payment system component)
* All other hosts in Store brach network segment (located at the same segment as POS)
* Paloalto and PFSense firewalls (essential network infrastructure)

Magento and Cyclos should be studied at application level to have greater knowledge about their functionality. If applications
use for example external database server it has impact on the scope of cardholder data environment.

# 4 Auditors #

Head auditors: Jouni, Petri.

Supplementary auditors: Pauli, Jani, Otso, Vesa, Pinja, Teemu and Janne.

Head auditors are responsible for the execution of the evaluation and possible focus changes during the evaluation.

# 5 Audit activities and schedule #

## 5.1 Schedule and premilinary work estimate ##

Premilinary work estimate:

 * Reviewing the material, planning and technical implementation: 32 h 
 * Review of administration and monitoring systems: 16 h 
 * Review of the ISMS including administration procedures and practices: 24 h 
 * Review of business continuity: 16 h 
 * Review of reporting procedures: 16 h 
 * Reporting: 16 h 
 * Total: 120 

## 5.2 Administrative and technical reviews of named technologies ##

### 5.2.1 Network and systems security ###

 1. Technical review
    * Review of firewall rules and configurations against the documentation using manual portscanning utilizing nmap and manual review of firewall policy configuration
    * Verification of documented zoning using scans and traffic capture collected with tcpdump
    
 2. Administrative review
    * Review of the change management process concerning router and firewall configuration changes
    * Secure and documented settings, including e.g. ports and protocols
    * Network diagrams
    * Administrative roles
    * Regular configuration review

### 5.2.2 Configuration defaults ###

 1. Technical review
    * Manual verification from configuration files that default passwords and other configuration parameters have been changed
    * Hardening of systems reviewed using Nessus agent and manual configuration checks
    * Separation of server roles reviewed manually by checking sudo and rbac configuration
    * Confirm that unnecessary protocols, services etc. have been disabled using manual checks, nmap and nessus
    * Review that secure administration channels are being utilized using traffic capture by tcpdump

 2. Administrative review
    * Configuration management

### 5.2.3 Data protection ###

 1. Technical review
    * Manual verification that no undocumented cardholder data persists in the systems
    * Manual verification that sensitive data is masked as depicted in the requirements
    * Manual verification that the security of encryption and encryption keys are sufficient

 2. Administrative review
    * Documentation of stored cardholder data

### 5.2.4 Security of data transmissions ###

 1. Technical review
    * Manual review of the configuration and analyzation of traffic capture generated by tcpdump to verify that required data is transferred properly encrypted

 2. Administrative review
    * Encryption strength
    * Encryption policies

### 5.2.5 Malware protection ###

 1. Technical review
    * Confirm that antivirus programs are installed in the necessary systems
    * Verify that antivirus programs are regularly updated
    * Manual verification that antivirus software can detect test malware

 2. Administrative review
    * Awareness of current virus and malware threath

### 5.2.6 Secure systems and applications ###

 1. Technical review
    * Confirm from logs that software updates are regularly applied
    * Confirm from e.g. Nessus logs that software is scanned for vulnerabilities
    * Confirm from e.g. Nessus logs that outer edge of network is scanned for vulnerabilities and undocumented services

 2. Administrative review
    * Update procedures for software
    * Identification of required updates
    * Regular software scans
    * Change control

### 5.2.7 Access restrictions to data ###

 1. Technical review
    * Manual review from system configuration that unnecessary access to cardholder data is prevented

 2. Administrative review
    * Documentation of access rights

### 5.2.8 Access restrictions to systems ###

 1. Technical review
    * Verify user identification from configurations
    * Verify limitations of user access from sudo or rbac configuration
    * Verify documented logging, connection and password policies

 2. Administrative review
    * User ID policy
    * Password policy
    * Training of personnel for secure settings

### 5.2.9 Monitoring and testing ###

 1. Technical review
    * Verification of generated audit logs
    * Confirm that separation of duties is applied to log systems
    * Verify log retention

 2. Administrative review
    * Audit log policy
    * Documented separation of duties

### 5.2.10 Testing security systems and processes ###

 1. Technical review
    * Manually confirm that IDS/IPS and HIDS exists and is correctly configured and the existing intrusion detection systems raise alarms during network testing

 2. Administrative review
    * Policy for regular testing, scanning and penetration testing
    * Existing scan reports

### 5.2.11 Information security policy ###

 1. Technical review

 2. Administrative review
    * Security policy
    * Risk assessment policy
    * Usage policies
    * Inventories and ownerships
    * Information security management
    * Training of personnel
    * Personnel screening
    * Incident response plan

# 6 Reporting #

 1. Schedule
    * Planning of the compliance audit
    * Execution of the compliance audit
    * Incident reporting during the audit concerning critical findings
    * Compliance audit wrapup and documentation delivery

 2. Reporting
    * Use the PCI DSS Reporting on compliance template (available at https://www.pcisecuritystandards.org/documents/PCI DSS-v3_2-ROC-Reporting-Template.pdf)
    * Audit author produces incident report from the possible findings and reports critical findings immediately when noticed.

 3. Distribution
    * Regulatory/Legislative authority when applicable
    * Acquirer
    * Requester or service provider when applicable
    
 4. Classification
    * Report is classified as secret, confidental or company confidental depending on audit target
   
