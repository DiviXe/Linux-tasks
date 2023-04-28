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

## 



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
- "The error message you received seems to be related to the Salt event bus, specifically the jobs.lookup_jid function. This error is not likely to be caused by a version mismatch between your Windows PC and the other Salt minions."
- Katsotaan saltin verio
- Salt näyttää olevan versio 3002.6 tmasterilla, joten versio on paljon vanhempi.
- ![image](https://user-images.githubusercontent.com/105793201/235191344-88154b00-1411-41c0-85ba-703ccc6370bf.png)
- Mietin ensiksi Saltin päivittämistä, mutta voi olla, että se tulisi liian työlääksi. Parempi on ladata Windowsille vahempi versio.
- Ensiksi poistetaan uusi version Windows minionilta.
- ![image](https://user-images.githubusercontent.com/105793201/235211711-db2b37fe-82d8-4433-9b34-4a268a38696d.png)
- Pitkän taistelun jälkeen sain vihdoin salt Minion 3002.6 version ladattua.
- ![image](https://user-images.githubusercontent.com/105793201/235218345-8a517da4-b64b-45c3-b8e3-0020d3017331.png)



## References
- https://terokarvinen.com/2023/palvelinten-hallinta-2023-kevat/, Tero karvinen, Palvelinten hallinta 2023
- https://terokarvinen.com/2018/control-windows-with-salt/, Tero karvinen Windows with salt
- https://developer.microsoft.com/en-us/windows/downloads/virtual-machines/, Windows 11 for VMBox
