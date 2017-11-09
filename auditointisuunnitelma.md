# Arviointisuunnitelma #
## Tietoj�rjestelm� X ##

-----

## Versiohistoria ##

-----

## Sis�lt� ##

-----

# 1 Johdanto #

Yleiskuvaus arvioinnin kohteena olevasta tietoj�rjestelm�st� tai tietoliikennej�rjestelyst�

Roolit (omistaja, k�ytt�j�t, toimittajat jos ulkoistettu palvelu)

# 2 Arvioinnin tavoite #

Arviointi/hyv�ksynt�: Arviointi

Arviointikriteerist�: PCI-DSS

Suojaustaso: N/A 

Arvioinnin arvioitu kesto, jos soveltuu: N/A

# 3 Soveltamisala #

Tarkistettavat organisaation yksik�t ja prosessit: LDILin maksukorttitietojen k�sittelyyn k�ytt�m�t j�rjestelm�t sek� niihin l�heisesti liittyv�t j�rjestelm�t.

Rajaukset

N�ytteenottosuunnitelma (jos soveltuu)

# 4 Arviointiryhm� #

P��arvioija:

Muut arvioijat:

(P��arvioijan vastuut, jos soveltuu)

# 5 Arviointitoiminnot ja aikataulu #

## 5.1 Aikataulu ja alustava ty�m��r�arvio #

Alustavan yhdess� XXX kanssa sovitun aikataulun mukaan...

Ty�m��r�arvio tarkastuksesta:

 * Aineistoon tutustuminen, suunnittelu sek� tekniset tarkastukset. Arvio:
 * Hallinta- ja valvontaj�rjestelm�n tarkastus ja liikenteen nauhoitus. Arvio:
 * Yll�pito-organisaation tietoturvallisuuden hallintaj�rjestelm� ja yll�pitomenettely. Arvio:
 * Varautumisen vaatimusten todentaminen. Arvio:
 * Raportointi. Arvio:
 * Yhteens�: 

(Mahdollista taulukkoa eri osa-alueista, esim. salausratkaisut, tekninen arviointi, passiivinen rajapinta-analyysi...: Henkil�t/Asiakkaan edustaja, vastuullinen arvioija, Arviointi/tarkastus pvm.)

## 5.2 Hallinnollinen arviointi ##

Todennusmenetelm�t:
 1. Turvallisuusdokumentaatioon tutustuminen
 2. Haastattelut

## 5.3 Tekninen arviointi ##

Todennusmenetelm�t:
 1. Passiivinen rajapinta-analyysi: ker�t��n verkkokauppaj�rjestelm�st� liikennett� tcpdumpilla tiedostoon analysoitavaksi.
 2. J�rjestelm�konfiguraatiot: tarkastellaan oleellisia konfiguraatioita automaattisesti sek� manuaalisesti.
 3. Aktiivinen rajapinta-analyysi: porttiskannaus ulkoa ja sis�verkosta k�sin
 4. Sovellusturvallisuus: skannataan nessuksella / openvassilla
 5. Salausratkaisut: site-to-site vpn-tunnelin salausasetusten tarkistus
 6. K�ytett�vyystestaukset: N/A
 7. Yhdysk�yt�v�ratkaisut: N/A
 8. Poikkeamanhavainnointikyky: Tarkistetaan ett� logia ker�t��n
 9. Fyysinen turvallisuus: N/A
 10. Hajas�teilysuojaukset: N/A
 11. Varautuminen: N/A

Osa-alueet
 1. Tietoliikenne
    	- palomuurien s��nn�st�t
	- vpn-yhdysk�yt�vien asetukset
	(Yksityiskohtainen selitys siit�, mit� tehd��n, esim. konfiguraatioihin tutustuminen. Lis�ksi tarkastettavat verkkolaitteet listattuna. Tarkastuksessa todennettavat osa-alueet, kuten esimerkiksi laitteiden k�ytt��notto ja poisto, verkkojen luokittelu ja erottelu, suodatus, salaus, poikkeamien valvonta ja havainnointi, varmenteet.
 2. Palvelimet
	- magento -palvelin
    (Yksityiskohtainen selitys siit� mit� tehd��n, esim. asetusten tarkastelu, skannaukset, testailut. Tarkastuksessa todennettavat osa-alueet: laiterekisteri, palvelinten k�ytt��notto ja poisto (ml. asennusohjeet ja kovennukset, sovellukset), P�ivitys- ja muutoshallinta, luokittelu, p��synvalvonta, haittaohjelmien suodatus, varmistukset, poikkeamahavainnointi, varmenteet, toipuminen)
 3. Levyj�rjestelm�t
 4. Hallintayhteydet
	- hallintayhteyksien turvallisuuden tarkastelu
5. Lokiratkaisut
	- tarkistetaan logien muodostuminen ja s�ilytys
 6. Poikkeamienhallinta ja -havainnointi
	- tarkistetaan logien muodostuminen ja s�ilytys
 7. Varmistukset
 8. Tunnistamismenetelm�t
	- tarkistetaan verkkokaupan autentikointi 
 9. Laitteiden ja j�rjestelmien toimitus- ja tuotantoketju

# 6 Raportointi #

P�yt�kirjat

Loppuraportti


JAKELU
