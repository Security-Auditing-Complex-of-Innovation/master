# Audit plan #
## Information system X ##
Miespoliisi 2.0
-----

## Change log ##

-----

## Contents ##

-----

# 1 Introduction #

General overview of the system being audited and the related connectivity arrangements.

Roles (owner, users, suppliers - if outsourced)

Target of this evaluation is LDIL's systems related to customer and payment information. Ldil is a national e-tailing company and it also has one physical store with POS-system.

Scope of the evaluation includes systems directly related to customerdata. These systems are web-store, extranet, accounting system, logging system and physical store POS-system.

# 2 Audit target #

Evaluation/Certification: Evaluation

Audit criteria: PCI-DSS

Protection level: N/A 

Timeframe of the audit: N/A

# 3 Applicability #

Parts of organization and processes that are being audited: Systems used by LDIL for managing payment card transactions and other closely related interfaces.

Scopings:

Sampling plan (if applicable)

PCI DSS requirements apply to organizations or entities that store, process or transmit cardholder data or sensitive authentication data. LDIL is an E-commerce company that administers their own E-commerce platform and point of sale systems at their branch store, thus making LDIL's payment system applicable to PCI DSS requirements. 

Storage of sensitive authentication data is forbidden by PCI DSS. On top of PCI DSS requirements, payment card brands can have their own instructions whether storage is permitted prior to authorization. Individual payment card brands requirements are left out the scope of this audit and focus is kept on PCI DSS requirements.

3.1 Scoping

Purpose of scoping is to determine which components of LDIL's business environment are part of cardholder data environment. Cardholder data environment comprises of LDIL's payment system components and all other connected systems.

Determining the scale of cardholder data environment is done by reviewing LDIL's provided documentation of the current business environment and security measures. Once the cardholder data environment and cardholder data flow in the payment system is identified and documented, the determined PCI DSS scope is reviewed by the LDIL before beginning the assesment (at least in real life case). 

LDIL cardholder data environment (according to LDIL documentation fig. 1, page 8):

* Magento server (E-commerce platform, payment system component)
* All other hosts in DMZ network segment (located at the same segment as Magento)
* POS Cyclos (payment system component)
* All other hosts in Store brach network segment (located at the same segment as POS)
* Paloalto and PFsense firewalls (essential network infrastructure)

Magento and Cyclos should be studied at application level to have greater knowledge about their functionality. If applications
use for example external database server it has impact on the scope of cardholder data environment.

# 4 Auditors #

Head auditor(s):

Supplementary auditors:

(Pääarvioijan vastuut, jos soveltuu)

# 5 Audit activities and schedule #

## 5.1 Schedule and premilinary work estimate #

Alustavan yhdessä XXX kanssa sovitun aikataulun mukaan...

Premilinary work estimate:

 * Reviewing the material, planning and technical implementation:
 * Review of administration and monitoring systems:
 * Review of the ISMS including administration procedures and practices:
 * Review of business continuity:
 * Review of reporting procedures:
 * Reporting:
 * Total:

(Mahdollista taulukkoa eri osa-alueista, esim. salausratkaisut, tekninen arviointi, passiivinen rajapinta-analyysi...: Henkilöt/Asiakkaan edustaja, vastuullinen arvioija, Arviointi/tarkastus pvm.)

## 5.2 Administrative review ##

Verification methods:
 1. Review of provided documentation concerning information security
 2. Interviews

## 5.3 Technical review ##

Verification methods:
 1. Passive, network analysis: kerätään verkkokauppajärjestelmästä liikennettä tcpdumpilla tiedostoon analysoitavaksi.
 2. Järjestelmäkonfiguraatiot: tarkastellaan oleellisia konfiguraatioita automaattisesti sekä manuaalisesti.
 3. Aktiivinen rajapinta-analyysi: porttiskannaus ulkoa ja sisäverkosta käsin
 4. Sovellusturvallisuus: skannataan nessuksella / openvassilla
 5. Salausratkaisut: site-to-site vpn-tunnelin salausasetusten tarkistus
 6. Käytettävyystestaukset: N/A
 7. Yhdyskäytäväratkaisut: N/A
 8. Poikkeamanhavainnointikyky: Tarkistetaan että logia kerätään
 9. Fyysinen turvallisuus: N/A
 10. Hajasäteilysuojaukset: N/A
 11. Varautuminen: N/A

Osa-alueet
 1. Tietoliikenne
    	- palomuurien säännöstöt
	- vpn-yhdyskäytävien asetukset
	(Yksityiskohtainen selitys siitä, mitä tehdään, esim. konfiguraatioihin tutustuminen. Lisäksi tarkastettavat verkkolaitteet listattuna. Tarkastuksessa todennettavat osa-alueet, kuten esimerkiksi laitteiden käyttöönotto ja poisto, verkkojen luokittelu ja erottelu, suodatus, salaus, poikkeamien valvonta ja havainnointi, varmenteet.
 2. Palvelimet
	- magento -palvelin
    (Yksityiskohtainen selitys siitä mitä tehdään, esim. asetusten tarkastelu, skannaukset, testailut. Tarkastuksessa todennettavat osa-alueet: laiterekisteri, palvelinten käyttöönotto ja poisto (ml. asennusohjeet ja kovennukset, sovellukset), Päivitys- ja muutoshallinta, luokittelu, pääsynvalvonta, haittaohjelmien suodatus, varmistukset, poikkeamahavainnointi, varmenteet, toipuminen)
 3. Levyjärjestelmät
 4. Hallintayhteydet
	- hallintayhteyksien turvallisuuden tarkastelu
5. Lokiratkaisut
	- tarkistetaan logien muodostuminen ja säilytys
 6. Poikkeamienhallinta ja -havainnointi
	- tarkistetaan logien muodostuminen ja säilytys
 7. Varmistukset
 8. Tunnistamismenetelmät
	- tarkistetaan verkkokaupan autentikointi 
 9. Laitteiden ja järjestelmien toimitus- ja tuotantoketju

# 6 Reporting #

Meeting minutes

Report


DISTRIBUTION
