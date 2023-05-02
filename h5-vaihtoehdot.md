# Tehtävä X) Lue ja tiivistä saltti Windowsille

## Saltti windowsille
- Artikkeli käsittelee miten Windows koneesta tehdään salt master.
- Ensiksi hommataan uusin ja puhdas versio Saltista Master koneelle tietyillä komennoilla
- Lisätään kyseiset avaimet ja koodit Master Windows koneelle, joten orja koneet toimivat myöhemmin.
- Hyväksytään orjat
- Hyväksytään saltin Windowsin asennusten repositoryt
- Asennetaan ohjelma esim. Firefox, Steam, Inkscape
- Ajetaan powershell komentoja
- Tämän jälkeen voimme "Admin" tilassa ajaa Salttia powershellin avulla lokaalisti
- Ladataan lisää paketteja chocolatelyllä
- Windows statella lisää ohjelmistoja

## Saltti Windowsille H5, P seppänen 2018
- Ladataan windows virtuaalikone
- Ladataan Windowsille vanhempi versio saltista
- Laitetaan masterin Ip-osoite salt minionin latauksen yhteydessä (muuten ei toimi jos ei tehdä oikein!)
- Katsotaan avaimista masterilta, että tuliko windows orja paikalle.
- Hyväksytään avain ja välitetään pkg.install gitti
- Oho! Ei toiminut, Windows koneelle pitää antaa paketit orjakoneelta, jotta lataukset saadaan toimimaan.
- Pakettien jälkeen asennus toimii ja windows kone pelittää!
- Infraa koodilla on myös mahdollista eli scriptien tekeminen esim chocolateyn kautta.


#  Aloitetaan Windows virtuaali koneen asentaminen VM boxiin. 
- Menin sivustolle https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/
- ja latasin Windowsin Virtualboxille
- ![image](https://user-images.githubusercontent.com/105793201/235140439-020b953b-c3c7-4b92-bd56-c450c7bf0037.png)
- ![image](https://user-images.githubusercontent.com/105793201/235142779-30ad1842-35eb-418d-8df5-1917b4ec8fec.png)
- Pitkän latauksen jälkeen puran paketin ja yritän laittaa sitä VirtualBoxiin.
- Windows 11 onnistuneesti ladattu
- ![image](https://user-images.githubusercontent.com/105793201/235158650-5c2dc9e8-23e1-4406-8223-0cc8fb358226.png)

# A) Ladataan Salt Windows 11 virtuaali koneelle
- Mennään sivustolle 
- https://docs.saltproject.io/salt/install-guide/en/latest/topics/install-by-operating-system/windows.html
- Ladataan AMD64-Setup.exe
- ![image](https://user-images.githubusercontent.com/105793201/235160631-a2f9dabd-e434-4b45-8630-e1c583e90c49.png)
- Setupissa laitetaan MASTER IP:ksi nimen omaan saltdemo_tmasterin IP, jotta windows minion saa yhteyden masteriin.
- ![image](https://user-images.githubusercontent.com/105793201/235161738-0774c49c-d2c3-4035-b15b-32048f50bc74.png)
- Annetaan Salt minion installerin nyt raksuttaa..
- ![image](https://user-images.githubusercontent.com/105793201/235161970-b3feec3b-ca2d-483d-842b-eb249f013649.png)
- ![image](https://user-images.githubusercontent.com/105793201/235164748-895ca965-1134-4eef-b497-27fa4ce4296b.png)
- Salt minion asennettu.
- Katsotaan mitä masterille kuuluu seuravaaksi. Komennolla **sudo salt-key** , jolla näämme kaikki olemassa olevat avaimet. 
- ![image](https://user-images.githubusercontent.com/105793201/235165585-fde7e8aa-66a0-4285-ab0f-12f72e2cd8d3.png)
- Windowsin avainta ei ole vielä näkyvissä. 
- Käynnistän virtuaali koneen uudestaan.
- Huomasin myös, että Windows_salt koneella ei ollut Adapter 2 Host only adapteria päällä (mikä on sama kuin virtuaalikoneilla, joten otin sen myös käyttöön. Tämä johtui ehkä siitä, että avaimeen ei päästy käsiksi.
- ![image](https://user-images.githubusercontent.com/105793201/235166754-9de2ac49-a70a-41a0-9fa4-56d6a88ad8cb.png)
- Nyt on aika käynnistää kone uudestaan.
- Koneen käynnistyksessä menee erittäin paljon aikaa.
- Windows kone löytyy nyt hyväksymättömistä avaimista!
- ![image](https://user-images.githubusercontent.com/105793201/235168730-fe74ad7c-a90e-4738-82f4-94bc8d9981c1.png)
- Hyväksytään avain ja kutsutaan windows perheeseen. **$ sudo salt-key -A**
- ![image](https://user-images.githubusercontent.com/105793201/235169119-8ea4b13f-26c0-413b-a73c-1ba31c36845e.png)

# B) Ei voi kalastaa. Käytä Windowsilla Salttia paikallisesti ilman verkkoa (Ruma-X, powershell as admin, salt-call --local state.single ...)
- Mennään windows koneen sisälle tarkastelamaan komentoja.
- Avataan powershelli Adminina.
- ![image](https://user-images.githubusercontent.com/105793201/235169600-91054e64-ce8e-488f-adad-0678a4ad1adb.png)
- Tehdään salt-call, jolla katsomme onko apache2 demoni ladattu Windowsille.
- ![image](https://user-images.githubusercontent.com/105793201/235174030-ff4accde-57a2-44bb-995b-59ce1918cf0f.png)
- Eipä taida olla, nyt tiedämme ainakin, että se pitää asentaa. Vastaus False tarkoittaa, että ohjelmaa ei ole asennettu.
- Katsotaan mitä Ohjelmia Windows 11 sisältää. 
- ![image](https://user-images.githubusercontent.com/105793201/235174726-d7b882a2-36fa-45f8-bb46-4390d452eb34.png)
- Tässä onkin iso listaa, testataan onko UserManager olemassa varmuuden vuoksi. 
- Näkyy olevan! Vastaus True tarkoittaa, että ohjelma on olemassa.
- ![image](https://user-images.githubusercontent.com/105793201/235174984-e8fa1f6d-17dc-449b-ac9e-77fa0860bf8d.png)

# C) Hei ikkuna! Tee hei maailma Windowsin Saltille. Voit vaikkapa tehdä tyhjän tiedoston johonkin väliaikaistiedostojen kansioon. Käytä idempotentteja komentoja, esim file.managed.
- Mennään takaisin vagrant@tmasterille ja salt kansioon johon luodaan uusi script tiedosto Windows Konetta varten.
- Loin kansion nimeltä Windowscripts /srv/salt hakemistoon.
- ![image](https://user-images.githubusercontent.com/105793201/235179605-4e312a9f-2e02-42f5-aa50-fdea568aa169.png)
- Seuraavaksi luodaan init.sls tiedosto johon tehdään scriptejä. Komennolla **sudo nano /srv/salt/windowscripts/init.sls**
- Luodaan scripti init.sls joka hakee moiwindows.txt:in salt kansiosta windowscripts
- ![image](https://user-images.githubusercontent.com/105793201/235181006-59ee6d7c-a135-4348-9c0f-c169942b4b09.png)
- Luodaan moiwindows.txt
- ![image](https://user-images.githubusercontent.com/105793201/235181231-ba8bee39-4752-4ee3-a50d-84d957c679cc.png)
- Testataan tekstitiedoston lähettämistä Windows orjalle komennolla **sudo salt 'Windows_salt' state.single init.sls**
- ![image](https://user-images.githubusercontent.com/105793201/235182175-02561ad7-4900-403d-aafa-1f5f34932675.png)
- En saanut yhteyttä Windows koneeseen. 
- Katsotaan error message. "salt-run jobs.lookup_jid 20230428145647047975"
- Googlailun jälkeen kyseessä on vissiin versio ongelma. 
- Sain tiedon ihan eri asiaan liittyen sivulta https://stackoverflow.com/questions/74733591/centos-salt-minion-cant-connect-to-salt-master-on-debian-sign-in-attempt-fail, mutta kommentissa luki, että "3004.1 minions are not able to communicate with masters older than 3004.1. You must upgrade your masters before upgrading minions. The same applies to any minions newer than 3004.1" , josta päättelin, että kyseessä on versio ongelma.
- "The error message you received seems to be related to the Salt event bus, specifically the jobs.lookup_jid function. This error is not likely to be caused by a version mismatch between your Windows PC and the other Salt minions."
- Katsotaan saltin verio
- Salt näyttää olevan versio 3002.6 tmasterilla, joten versio on paljon vanhempi.
- ![image](https://user-images.githubusercontent.com/105793201/235191344-88154b00-1411-41c0-85ba-703ccc6370bf.png)
- Mietin ensiksi Saltin päivittämistä, mutta voi olla, että se tulisi liian työlääksi. Parempi on ladata Windowsille vahempi versio.
- Ensiksi poistetaan uusi version Windows minionilta.
- ![image](https://user-images.githubusercontent.com/105793201/235211711-db2b37fe-82d8-4433-9b34-4a268a38696d.png)
- Pitkän taistelun jälkeen sain vihdoin salt Minion 3002.6 version ladattua.
- ![image](https://user-images.githubusercontent.com/105793201/235218345-8a517da4-b64b-45c3-b8e3-0020d3017331.png)
- Kone on elossa!
- ![image](https://user-images.githubusercontent.com/105793201/235222547-e79b95ea-21cf-4719-abc4-19ae1fac7484.png)
- Pusketaan muutokset uudestaan **sudo salt 'Windows_salt' state.single init.sls**
- Jostain syystä salt ei tunnistanut, että scriptini init.sls oli salt kansiossa windowscripts.
- ![image](https://user-images.githubusercontent.com/105793201/235227377-7a4c8630-de24-4559-94a4-524058e39c61.png)
- Komennolla **$ sudo salt 'windows_salt' state.apply windowscripts.init** oletettiin, että windowscripteissä oli init tiedosto ja tällä sitten se meni läpi windowsille.
- ![image](https://user-images.githubusercontent.com/105793201/235227493-88a91842-648b-4eea-957e-28f36e8d33a8.png)
- Tarkistetaan idempotenttisuus
- ![image](https://user-images.githubusercontent.com/105793201/235227912-0ffdc512-808a-4daa-aa62-433cd3cb5f65.png)
- Katsotaan onko Windows koneella tiedosto
- ![image](https://user-images.githubusercontent.com/105793201/235228011-0757f3e8-0b17-4b62-bd91-4d0afb9b8d79.png)
- Näyttää olevan!
- ![image](https://user-images.githubusercontent.com/105793201/235228136-9924c256-6244-4c15-9b72-2d3001cdb815.png)
- Text editor näyttää mustaa, mutta tiedosto on kuitenkin olemassa ja tekstikin on paikallaan.

# D) Installed. Asenna Windowsille ohjelma Saltilla. (Voit käyttää eri vaihtoehtoja: kopioida binäärin suoraan sopivaan kansioon, pkg.installed ja choco, pkg.installed ja salt winrepo).
- Asennetaan vaikka choco.
- Tehdään Teron Control Windows With Salt artikkelin mukaisesti "Enable Salt Windows Software Repositories", koska kansioni on nimeltään windowscripts, joten anna tälle kansiolle oikeudet.
- Tehdään vastaavat komennot:
- **sudo mkdir /srv/salt/win**
- **sudo chown root.salt /srv/salt/win**
- **sudo chmod ug+rwx /srv/salt/win**
- Nyt päivitetään Windows repositiot (lisää selityksiä myöhemmin) 
- **sudo salt-run winrepo.update_git_repos**
- **sudo salt -G 'os:windows' pkg.refresh_db**
- ![image](https://user-images.githubusercontent.com/105793201/235230285-af0adcab-1929-456f-9525-08cc2e7b34c6.png)
- Päivitykset tulleet onnistuneesti
- Tehdään uusi init.sls tiedosto, jolle paketinhallinnan kautta pistetään ohjelmia läpi. 
- Kokeillaan gitin ja nginxin asennusta.
- ![image](https://user-images.githubusercontent.com/105793201/235230928-eafc49ed-69a1-4d8b-942c-d794a35ead37.png)
- ![image](https://user-images.githubusercontent.com/105793201/235231346-2b890b2b-2181-4a02-9b15-c15225c777d4.png)
- nginx ei tullut ladattua onnistuneesti, tämä on varmasti sen takia kun laitoin ne samaan. Kokeillaan uudestaan ilman nginxiä.
- ![image](https://user-images.githubusercontent.com/105793201/235231867-dc23b9b5-bdd9-4297-b119-7c129a0690bf.png)
- Gittikään ei onnistunut, mutta tämä johtuu ehkä siitä, että git on jo tietokoneella. 
- Onko tähän lataukseen joku syy?
- ![image](https://user-images.githubusercontent.com/105793201/235231946-a728126c-a37f-4eaa-9044-93a65c2334c1.png)
- Gittihän se siellä.
- Kokeillaan choholatelyn lataus pkg.installilla.
- ![image](https://user-images.githubusercontent.com/105793201/235232528-d08963cc-f8d0-46a5-9b07-74fb3d4270c9.png)
- Lataus onnistui
- Tehtävä osittain valmis, jostain syystä notepad++ lataaminen ei onnistunut chocon kautta. Mikä syynä?
- Kokeilin vielä päivittää windows_salt koneen paketit, mutta ei auttanut.
- ![image](https://user-images.githubusercontent.com/105793201/235430484-77224f33-22d9-408f-9ab6-c126410dbb58.png)
- ![image](https://user-images.githubusercontent.com/105793201/235430541-0230024f-6b1c-4e88-a49a-db6736e6659b.png)





## References
- https://terokarvinen.com/2023/palvelinten-hallinta-2023-kevat/, Tero karvinen, Palvelinten hallinta 2023
- https://terokarvinen.com/2018/control-windows-with-salt/, Tero karvinen Windows with salt
- https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/, Windows 11 for VMBox
- https://stackoverflow.com/questions/74733591/centos-salt-minion-cant-connect-to-salt-master-on-debian-sign-in-attempt-fail, Salt-minion cant connect to salt master, Virheenpäättely esimerkki
- https://pseppanen296518693.wordpress.com/, P seppänen Windows raportti
