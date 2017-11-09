# Arviointisuunnitelma #
## Tietojärjestelmä X ##

-----

## Versiohistoria ##

-----

## Sisältö ##

-----

# 1 Johdanto #

Yleiskuvaus arvioinnin kohteena olevasta tietojärjestelmästä tai tietoliikennejärjestelystä

Roolit (omistaja, käyttäjät, toimittajat jos ulkoistettu palvelu)

# 2 Arvioinnin tavoite #

Arviointi/hyväksyntä: Arviointi

Arviointikriteeristö: PCI-DSS

Suojaustaso: N/A 

Arvioinnin arvioitu kesto, jos soveltuu: N/A

# 3 Soveltamisala #

Tarkistettavat organisaation yksiköt ja prosessit: LDILin maksukorttitietojen käsittelyyn käyttämät järjestelmät sekä niihin läheisesti liittyvät järjestelmät.

Rajaukset

Näytteenottosuunnitelma (jos soveltuu)

# 4 Arviointiryhmä #

Pääarvioija:

Muut arvioijat:

(Pääarvioijan vastuut, jos soveltuu)

# 5 Arviointitoiminnot ja aikataulu #

## 5.1 Aikataulu ja alustava työmääräarvio #

Alustavan yhdessä XXX kanssa sovitun aikataulun mukaan...

Työmääräarvio tarkastuksesta:

 * Aineistoon tutustuminen, suunnittelu sekä tekniset tarkastukset. Arvio:
 * Hallinta- ja valvontajärjestelmän tarkastus ja liikenteen nauhoitus. Arvio:
 * Ylläpito-organisaation tietoturvallisuuden hallintajärjestelmä ja ylläpitomenettely. Arvio:
 * Varautumisen vaatimusten todentaminen. Arvio:
 * Raportointi. Arvio:
 * Yhteensä: 

(Mahdollista taulukkoa eri osa-alueista, esim. salausratkaisut, tekninen arviointi, passiivinen rajapinta-analyysi...: Henkilöt/Asiakkaan edustaja, vastuullinen arvioija, Arviointi/tarkastus pvm.)

## 5.2 Hallinnollinen arviointi ##

Todennusmenetelmät:
 1. Turvallisuusdokumentaatioon tutustuminen
 2. Haastattelut

## 5.3 Tekninen arviointi ##

Todennusmenetelmät:
 1. Passiivinen rajapinta-analyysi: kerätään verkkokauppajärjestelmästä liikennettä tcpdumpilla tiedostoon analysoitavaksi.
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

# 6 Raportointi #

Pöytäkirjat

Loppuraportti


JAKELU
