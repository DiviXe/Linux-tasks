# Tehtävä 1 h1-suolaa 

(Läksyn lukijalle tosiaan ensimmäinen kertani Linuxin parissa.) 

# X) Lue ja tiivistä.

## Karvinen2023: Create a Web Page Using Github</h3>
- Registeröidy Githubiin
- Luo oma repositorysi ylänurkasta
-  (lisää README.md tiedosto repositoryn sisään)
- lisää .md loppu tiedostosi perään
- kirjoita tekstiä ja commit.
- Sivusi on nyt luotu.
- file h1-suolaa.md luotu github repoon.
## Karvinen2023: Salt Vagrant - automatically provision one master and two slaves</h3>
- Ensiksi asennetaan virtuaali ympäristö komennoilla: 
- $ sudo apt-get update
- $ sudo apt-get -y install virtualbox vagrant micro
- $ mkdir saltdemo; cd saltdemo
- $ micro Vagrantfile

- Tämän jälkeen copypastetaan valmiina olevat Vagrantfilet kolmelle koneelle.
- Bootataan koneet komennolla $ vagrant up
- Hyväksytään koneet ensiksi komennolla $ vagrant ssh tmaster ja tämän jälkeen $ sudo salt-key -A
- Tämän jälkeen koneet pitää hyväksyä kirjoittamalla Y ja enter. 
- Tästä saa tiedotteen Key for minion t001 accepted. Key for minion t002 accepted.
- Testataan onko koneet hengissä $ sudo salt '*' test.ping
- Voit komentaa orjia komennolla $ sudo salt '*' cmd.run 'hostname -I'
- Tärkeää tietoa koneista voidaan kerätä komennolla $ sudo salt '*' grains.items (esim ip osoitteen ja käyttöjärjestelmän.
- Idempotenttikomennot esimerkiksi $ sudo salt '*' state.single file.managed '/tmp/see-you-at-terokarvinen-com' ensiksi tulee "Succeeded: 1 (changed=1) 
- Tämän jälkeen komennon voi uudestaan ajaa ja changed pitäisi olla =0. IDEMPOTENTTISUUS ON KAIKISTA TÄRKEINTÄ!
- Ohjelmistoja voidaan myös ladata esim. $ sudo salt '*' state.single pkg.installed apache2
- Pitää varmistaa, että demoni on käynnissä $ sudo salt '*' state.single service.running apache2 
- - otetaan userit käyttöön esim. $ sudo salt '*' state.single user.present terote01

- Koodia voidaan myös kirjoittaa teksti tiedostoon
- esim. $ sudo mkdir -p /srv/salt/hello
- $ sudoedit /srv/salt/hello/init.sls
- Syntaxina on YAML eli tabeja ei voida käyttää.





# A) Asenna Debian 11 Vagrantilla.
![image](https://user-images.githubusercontent.com/105793201/228643756-3686698a-0981-4bf9-b954-a3d44c23ec38.png)
- Debian ladattu onnistuneesti VM boxiin. 

# B) Asenna artikkelissa (Karvinen 2023) kuvattu kolmen koneen verkko

Erroreita, ongelma on siinä, että virtualbox ei ole asennettu kunnolla tai joku versio ei ole yhteensopiva. 
![image](https://user-images.githubusercontent.com/105793201/228932436-12349995-28c5-4b81-91b4-3f5a9ab48420.png)

- Kaikki asennukset tehty uudestaan
![image](https://user-images.githubusercontent.com/105793201/229061525-2a055ffc-e3a0-4c65-ad61-6e5c1ce07824.png)

-Asennusten jälkeen lataukset toimii, paitsi nyt vagrantfilessä Code_EACCESS DENIED Error 

- ongelma tulee kun yrittää saada virtuaalikoneet päälle kirjoittamalla "vagrant up" 
-![image](https://user-images.githubusercontent.com/105793201/229091362-5b7c838f-2bac-4ca9-9f90-699f23cd9edf.png)
- kokeiltu virtualboxia 7.0, herjaa error, että vagrantfile toimii vain virtualbox 6.1 tai vanhemmalla versiolla.
- 6.1 latauksen jälkeen tämä error tulee. 
- Yritin löytää netistä tietoa, jotkut sanoivat, että tämä ongelma liityy virtualboxin asetuksiin.  

# B) Yritetään saada virtuaalikoneet päälle uudestaan komennolla vagrant up .. 4.4.2023 22:20

![image](https://user-images.githubusercontent.com/105793201/229898216-ab1709c5-ad12-45a7-a618-13b300f537ce.png)
- Error on edelleen sama "Code E_ACCESSDENIED (0x90070005) , yritetään ratkaista asiaa

- koneet käyttävät nyt eri ip-osoiteavaruutta kuin määrittelyssä, eli muokattiin osoitteet 192.168.12.0/24 -> 192.168.56.9/24 muotoisiksi.
- Nyt ilmeni uusi virhe, "VBoxManage VT-X is not available, tämä liittyisi virtualisointiin. 
- ![image](https://user-images.githubusercontent.com/105793201/229913974-bf4db634-2138-439e-8b64-d9e91997799b.png)
# Yritin uudelleen asentaa virtualboxia, mutta ei toiminut, siirryn nyt kokeilemaan windows powershelliä huomenna, 5.4.2023 0.09
- Uusi päivä testataan windowsin powershellin kanssa.

# Vóila! virtuaalikoneiden asennus onnistui!

![image](https://user-images.githubusercontent.com/105793201/230014491-ec1f4305-188d-426c-91ee-822846cb838f.png)

# C) Hyväksytään orjat ja testataan yhteys.

- Kirjaudutaan pääkäyttäjälle ja hyväksytään orjat
- vagrant ssh tmaster
- $ sudo salt-key -A
- -![image](https://user-images.githubusercontent.com/105793201/230015024-faa4854c-2d09-48bb-93bc-b85dd6da9730.png)
-![image](https://user-images.githubusercontent.com/105793201/230015737-1730ed8c-a120-49e3-af8c-3cd76c3bafaa.png)

- Testataan vastaavatko orjat takaisin masterilla pingaamalla koneita, eli sanomalla HEI oletteko siellä. 
- ![image](https://user-images.githubusercontent.com/105793201/230016775-4d1ff4c3-5002-4d84-8fa2-927bcfc3e981.png)
- Vastaus on True eli kyllä ollaan.

# D) Näytä esimerkit seuraavista tiloista: package, file, service, user, cmd.run. (voit käyttää state.single)
- Ensiksi keräsin tietoa koodilla **$ sudo salt '*' grains.item osfinger ipv4**
- Ipv4 osoitteet näkyi ja käyttöjärjestelmät. 
- ![image](https://user-images.githubusercontent.com/105793201/230021313-e7d33198-0adc-4100-aa12-4e10e44c7444.png)

- asensin apache packagen molempiin virtuaalikoneisiin komennolla **$ sudo salt '*' state.single pkg.installed apache2**. 
- Asennus onnistui täydellisesti ja tämän jälkeen kokeilin vielä asentaa uudestaan, ettei mikään ole muuttunut. 
- ![image](https://user-images.githubusercontent.com/105793201/230022603-5febd0e7-d123-4f70-afa0-a3854798dc75.png)
- kaikki ovat **idempotenttisia.** 
- ![image](https://user-images.githubusercontent.com/105793201/230022761-14ffc376-ed19-4f8f-94d4-cb20767dad86.png) 

 ## References
 
 Karvinen 2023: https://terokarvinen.com/2023/create-a-web-page-using-github/, 
 https://terokarvinen.com/2020/command-line-basics-revisited/, 
 https://terokarvinen.com/2023/salt-vagrant/
