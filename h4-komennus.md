# Komennus tehtävä
- Tehtävän tekemiseen käytetty "kuuluisaa" Windows kymppiä ja PowerShelliä. 

# A) hello.sh. Tee oma shell script (bash, sh...) ja laita se kaikille käyttäjille.
- Käynnistetään virtuaalikoneet **vagrant up** :illa ja mennään master käyttäjälle perus kommennolla **vagrant ssh tmaster** 
- Sisällä ollaan.
- ![image](https://user-images.githubusercontent.com/105793201/233036664-4a6feac5-e849-4eb8-96a5-7b77d55b069d.png)
- Seuraavaksi luodaan scripti kansio nimeltä shine 
- **mkdir shine** ja mennään scripts kansion sisälle **cd shine**
- ![image](https://user-images.githubusercontent.com/105793201/233334481-02112c8d-db38-4b3f-b3f2-49c371fe394b.png)
- Nyt tehdään scripti tiedosto hello.sh kansion sisälle komennolla **nano hello.sh** ja laitetaan tiedosto kirjoittamaan shine. 
- ![image](https://user-images.githubusercontent.com/105793201/233334854-c9c616d9-1030-48c9-a3a6-18f96357d834.png)
- ![image](https://user-images.githubusercontent.com/105793201/233334926-c204eae4-caa3-423a-927f-d29ed5f96890.png)
- kokeillaan komentoa kansiossa
- ![image](https://user-images.githubusercontent.com/105793201/233335080-94185c43-0d65-428a-aff6-cfa9112d19da.png)
- "Permission denied, eli käyttöoikeuksia ei ole. pitää ajaa komento, jolla saadaan käyttöoikeudet kyseiselle koodille.
- Kirjoitetaan komento **chmod ugo+x hello.sh** , joka antaa oikeudet kaikille käyttäjille ja oikeudet pyörittää ohjelmaa. 
- Chmod ugo:ssa u tarkoittaa tiedoston omistajaa, g tarkoittaa tiedoston ryhmää ja o tarkoittaa muita käyttäjiä (other). + tarkoittaa oikeuksien lisäämistä ja x"tarkoittaa suoritusoikeutta. 
- ![image](https://user-images.githubusercontent.com/105793201/233335456-40bfbac7-71ce-44d4-8d8c-a92a1a2da21a.png)
- ongelmia ei ilmennyt joten komento onnistui.
- ![image](https://user-images.githubusercontent.com/105793201/233338245-032d1552-d535-4489-aff3-f162ad135cfa.png)
- Scripti toimii nyt oletetussa kansiossa shine.  
- Luon nyt uuden kansion roottiin, /usr/local/bin/ johon liitän minun hello.sh scriptin. 
- sudo mkdir **/usr/local/bin/runit**
- ![image](https://user-images.githubusercontent.com/105793201/233338913-06806054-aaaa-4c16-b201-37660d8746a8.png)
- Tiedosto on kuitenkin tyhjä joten ehkä tämä on syy miksi en nää sitä ls komennolla. 
- ![image](https://user-images.githubusercontent.com/105793201/233340250-5940c573-aed7-4971-be31-63f1bbbe0388.png)
- tiedosto meni perille ja tarkistin vielä, että shine kansiossa on scripti hello. Tarkistan nyt asian root kansiosta.
- ![image](https://user-images.githubusercontent.com/105793201/233340399-e8333197-f18a-4f8e-998c-208b15edc260.png)
- tiedosto näyttää olevan sielläkin. Testataan koodia!
- ![image](https://user-images.githubusercontent.com/105793201/233340754-2e1de5ab-46dc-434d-8ac7-46dab592d5ea.png)
- Koodi ei näyttänyt toimivan. Etsitään vika. 
-Päättelin, että vikana oli kansion runit oikeudet vaikka kansio olibin rootissa, joten lisäsin hello.sh tiedoston suoraan /usr/local/bin kansiostoon ja koodi toimi!
- käytin komentoa **sudo cp ~/shine/hello.sh /usr/local/bin/** 
- ![image](https://user-images.githubusercontent.com/105793201/233341846-38eb86bc-ae88-450c-8ac9-9e950ae53c64.png)
- Runit kansion tekeminen oli siis täysin turhaa.

# B) pythonhello.py. Tee oma Python-skripti ja laita se kaikille käyttäjille.
- Python scriptin tekeminen pitäisi olla helppoa, aloitetaan menemällä uudestaan shine kansioon ja luodaan pythonhello.py script tiedosto. **nano pythonhello.py**
- ![image](https://user-images.githubusercontent.com/105793201/233342242-0d6c8bbf-b48a-43cf-a02f-8aa1b88c2e4c.png)
- ![image](https://user-images.githubusercontent.com/105793201/233342102-c9af6013-8e9b-4cf1-8f27-270b9b86bff8.png)
- Tarkistan varmuuden vuoksi pythonin version komennolla python --version
- koneessa on python 3.9.2 versio
- ![image](https://user-images.githubusercontent.com/105793201/233342947-fed27575-79cc-4a8e-b474-5206ba14497d.png)
- Valitettavasti pythonhello:a ei pystytty ajamaan ja scripti näkyy valkoisena, koska tiedostolla ei ole oikeuksia.
- ![image](https://user-images.githubusercontent.com/105793201/233343189-12342e15-9b84-43b8-bcc8-5583e196ba04.png)
- lisätään oikeudet komennolla **chmod ugo+x pythonhello.py**
- Tarkastellaan kansiota uudestaan ja ajetaan komento.
- ![image](https://user-images.githubusercontent.com/105793201/233343462-fe22fa3a-ff0b-4628-8392-ef703ddd4152.png)
-  Vihreä on jo parempi! Eli oikeudet näkyy olevan ja komento toimii!
-  Nyt lisätään se roottin ja katsotaan miten se toimii.
-  ![image](https://user-images.githubusercontent.com/105793201/233343815-fd74c2c4-855c-41e6-aa3c-0ae2fb741054.png)
- Komento tomii täydellisesti kaikkialla!

# C) Automatisoi näiden skriptien asennus orjille Saltilla.
- Nyt laitetaan koodit orjille. 
- luodaan uusi salt tiedosto kansio tasks ja luodaan sinne scripti joka lähettää tiedostot orjakoneilla ja määritellään oikeudeksi mode: "0755" eli suoritusoikeudet.
- Ensin tehtiin kansio salttiin komennolla **$ sudo mkdir -p /srv/salt/tasks** tämän jälkeen mentiin itse kansioon ja laitettiin koodit paikoilleen.
- **sudoedit /srv/salt/tasks/task.sls**
- ![image](https://user-images.githubusercontent.com/105793201/233346861-f4a8af88-a6e0-4e65-9e46-1a04f6ffa009.png)
- koska tiedoston nimet oli hello.sh ja pythonhello.py otin molemmat mukaan rootista.
- Sourceksi tulee polku josta tiedosto lähtee minioneille.
- ![image](https://user-images.githubusercontent.com/105793201/233346542-8865d7e0-61ca-47d8-bc83-c6f53d6d49a4.png)
- Koodi näyttää olevan myös oikeassa paikassa
- ![image](https://user-images.githubusercontent.com/105793201/233346913-8e865896-bf3c-4709-babe-72213e28b406.png)

- testataan lähteekö koodi perille komennolla sudo salt '*' state.apply tasks/task
- ![image](https://user-images.githubusercontent.com/105793201/233347312-82375906-3433-4175-aacd-6db13ebc00e2.png)
- Erroria tuli, taitaa olla että koodissa oli väärästi laitettu polku.
- Ainiin, tietenkin unohtui tiedostojen kopiointi itse salttiin!
- ![image](https://user-images.githubusercontent.com/105793201/233348235-b0dfe3c7-8a38-4e0e-a454-931964263375.png)
- Tiedostoja ei näy tasks salt kansiossa, joten laitan tiedostot paikoilleen.
- ![image](https://user-images.githubusercontent.com/105793201/233348963-ceeb5439-ca51-4cd3-a3ce-2c3af1742c16.png)
- vaihdetaan myös source saltista tiedostoon **salt://tasks/**, koska tälloin mehän emme ole ottamassa tiedostoja "task.sls" tiedoston sisältä.
- ![image](https://user-images.githubusercontent.com/105793201/233349937-372ba0b3-0a96-4587-b205-0ee81f63f686.png)
- Kokeillaan uudestaan!
- ![image](https://user-images.githubusercontent.com/105793201/233350164-3017799f-b7eb-4ba0-92ec-76f4a201cbc0.png)
- mollemille koneille on luotu uudet tiedostot koneen sisään! Katsotaan vielä idempotenttisuus.
- Idempotenttisuus kunnossa, tiedostoja EI ladata uudestaan eikä mikään muutu järjestelmässä.
- ![image](https://user-images.githubusercontent.com/105793201/233350371-bf8aaa6f-b7e5-41fc-bf17-67d8d938ecb1.png)
- kokeillaan vielä scriptien ajaminen komennolla, **sudo salt '*' state.single cmd.run 'hello.sh ja hellopython.py'**
- Shine tulee näkyviin!
- ![image](https://user-images.githubusercontent.com/105793201/233350820-dd810875-f622-466f-bc60-2e5f4f2e4d68.png)
- Hello world! i am python snake! tulee näkyviin myös!
- ![image](https://user-images.githubusercontent.com/105793201/233350937-a0a3270b-1317-41bf-8cb7-9f0668315d15.png)
- Tehtävä suoritettu

# D) Asenna jokin yhden binäärin ohjelma Saltilla orjille.
- Asennetaan vaikka nano kommennolla **$ sudo salt '*' state.single pkg.installed name=nano** Name=nano niin se on varmasti nano editor eikä muu nano.
- ![image](https://user-images.githubusercontent.com/105793201/233352073-0568f350-ab13-43b0-baf7-a5e9e4e53419.png)
- Nano olikin jo asennettu, mutta ei se haittaa! Kokeillaan testata mikä versio nanossa on. (Nanon asennus olisi muuten onnistunut)
- ![image](https://user-images.githubusercontent.com/105793201/233352624-39c31387-de70-4b9f-a3c9-3d95d8b9e119.png)
- no eipä tullut kummosta ilmoitusta, kokeillaan kuitenkin cmd.runista vielä.
- ![image](https://user-images.githubusercontent.com/105793201/233352978-fcd70820-a360-428c-84d8-291e19ba8344.png)
- nanohan se siellä on.
## References: 
- https://terokarvinen.com/2018/control-windows-with-salt/, Tero Karvinen 2018, Contorl windows with salt
- https://terokarvinen.com/2023/palvelinten-hallinta-2023-kevat/, Tero karivnen 2023, Palvelinten hallinta 
- https://terokarvinen.com/2023/salt-vagrant/, Tero Karvinen 2023, Salt Vagrant
