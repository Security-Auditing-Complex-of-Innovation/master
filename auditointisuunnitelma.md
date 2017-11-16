# Audit plan #
## Information system X ##

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
