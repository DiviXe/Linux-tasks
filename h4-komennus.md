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
- käytin komentoa **sudo cp ~/shine/hello.sh /usr/local/bin/** (selitystä lisää)
- ![image](https://user-images.githubusercontent.com/105793201/233341846-38eb86bc-ae88-450c-8ac9-9e950ae53c64.png)
# B) hello.py. Tee oma Python-skripti ja laita se kaikille käyttäjille.
- Python scriptin tekeminen pitäisi olla helppoa, aloitetaan menemällä uudestaan shine kansioon ja luodaan pythonhello.py script tiedosto. ** nano pythonhello.py**
- ![image](https://user-images.githubusercontent.com/105793201/233342242-0d6c8bbf-b48a-43cf-a02f-8aa1b88c2e4c.png)
- ![image](https://user-images.githubusercontent.com/105793201/233342102-c9af6013-8e9b-4cf1-8f27-270b9b86bff8.png)
- Tarkistan varmuuden vuoksi pythonin version komennolla python --version
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
