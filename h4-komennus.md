# Komennus tehtävä
- Tehtävän tekemiseen käytetty "kuuluisaa" Windows kymppiä ja PowerShelliä. 

# A) hello.sh. Tee oma shell script (bash, sh...) ja laita se kaikille käyttäjille.
- Käynnistetään virtuaalikoneet **vagrant up** :illa ja mennään master käyttäjälle perus kommennolla **vagrant ssh tmaster** 
- Sisällä ollaan.
- ![image](https://user-images.githubusercontent.com/105793201/233036664-4a6feac5-e849-4eb8-96a5-7b77d55b069d.png)
- Seuraavaksi luodaan scripti kansio nimeltä shine 
- **mkdir shine** ja mennään scripts kansion sisälle **cd shine**
- ![image](https://user-images.githubusercontent.com/105793201/233334481-02112c8d-db38-4b3f-b3f2-49c371fe394b.png)
- Nyt tehdään scripti tiedosto hello.sh kansion sisälle komennolla ** nano hello.sh** ja laitetaan tiedosto kirjoittamaan shine. 
- ![image](https://user-images.githubusercontent.com/105793201/233334854-c9c616d9-1030-48c9-a3a6-18f96357d834.png)
- ![image](https://user-images.githubusercontent.com/105793201/233334926-c204eae4-caa3-423a-927f-d29ed5f96890.png)
- kokeillaan komentoa kansiossa
- ![image](https://user-images.githubusercontent.com/105793201/233335080-94185c43-0d65-428a-aff6-cfa9112d19da.png)
- "Permission denied, eli käyttöoikeuksia ei ole. pitää ajaa komento, jolla saadaan käyttöoikeudet kyseiselle koodille.
- Kirjoitetaan komento **chmod ugo+x hello.sh** , joka antaa oikeudet kaikille käyttäjille ja oikeudet pyörittää ohjelmaa. 
- ![image](https://user-images.githubusercontent.com/105793201/233335456-40bfbac7-71ce-44d4-8d8c-a92a1a2da21a.png)
- ongelmia ei ilmennyt joten komento onnistui.
- ![image](https://user-images.githubusercontent.com/105793201/233338245-032d1552-d535-4489-aff3-f162ad135cfa.png)
- Scripti toimii nyt oletetussa kansiossa shine.  
- Luon nyt uuden kansion roottiin, /usr/local/bin/ johon liitän minun hello.sh scriptin. 
- 
- ![image](https://user-images.githubusercontent.com/105793201/233041821-9e5c2909-9296-44bd-9fc2-f614d588a85b.png)
- Refereshataan envronment kansiosto komennolla **source /etc/environment** ja ajetaan komento hello.sh ilman sitä, että olemme root tiedostoissa. 
- ![image](https://user-images.githubusercontent.com/105793201/233042396-6afd4615-a80e-4039-b6ff-80eca95a7c3c.png)
- kaikki toimii oletuksen mukaisesti.
# B) hello.py. Tee oma Python-skripti ja laita se kaikille käyttäjille.
- Koska path variable on asetettu niin python scriptin tekeminen pitäisi olla helppoa, aloitetaan menemällä uudestaan script tiedostoihin ja luodaan pythonhello.py script tiedosto. **sudo nano pythonhello.py**
- Käytetään virtuaalikoneessa olevaa python environment kolmosta, jonka polku ilmoitetaan koodin alussa. 
- ![image](https://user-images.githubusercontent.com/105793201/233043552-6364df92-51ba-4a40-a26f-04fc1b4136af.png)
- katsotaan varmuuden vuoksi pythonin versio.
- koneessa on python 3.9.2 versio
- ![image](https://user-images.githubusercontent.com/105793201/233043705-3c186267-abe8-4e6c-bfa8-ce928897977f.png)
- hyväksytään scripti kaikille käyttäjille komennolla **sudo chmod +x pythonhello.py** 
- Hyväksyntä onnistui
- ![image](https://user-images.githubusercontent.com/105793201/233043916-8a7667cc-bd16-49aa-a1cc-02fbdd42f5d2.png)
- kokeillaan seuraavaksi toimiiko koodi oikein.
- ![image](https://user-images.githubusercontent.com/105793201/233045452-93845fe7-1e80-458d-a831-feb43c74bfbf.png)
- komento toimii
# C) Automatisoi näiden skriptien asennus orjille Saltilla.
- Nyt laitetaan koodit orjille. 
- TULOSSA PIAN
# D) Asenna jokin yhden binäärin ohjelma Saltilla orjille.



## References: 
- https://terokarvinen.com/2018/control-windows-with-salt/, Tero Karvinen, 2018
