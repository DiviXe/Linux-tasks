# Komennus tehtävä
- Tehtävän tekemiseen käytetty kuuluisaa Windows PowerShelliä. 

# A) hello.sh. Tee oma shell script (bash, sh...) ja laita se kaikille käyttäjille.
- Käynnistetään virtuaalikoneet **vagrant up** :illa ja mennään master käyttäjälle perus kommennolla **vagrant ssh tmaster** 
- Sisällä ollaan.
- ![image](https://user-images.githubusercontent.com/105793201/233036664-4a6feac5-e849-4eb8-96a5-7b77d55b069d.png)
- Seuraavaksi luodaan scripti kansio nimeltä scripts (Tiedosto menee roottiin eli sinne missä on kaikki tietokoneen sisäiset paketit ja käyttäjät.)
- **sudo mkdir /usr/local/bin/scripts** ja mennään scripts kansion sisälle **cd /usr/local/bin/scripts scripts**
- ![image](https://user-images.githubusercontent.com/105793201/233038101-9640628c-0c4d-46b7-84b3-e3b3ff7d0b77.png)
- Nyt tehdään scripti tiedosto hello.sh kansion sisälle komennolla **sudo nano hello.sh** ja laitetaan tiedosto kirjoittamaan shine. 
- ![image](https://user-images.githubusercontent.com/105793201/233038888-f7f05a87-1e2a-4ad6-a748-c06a0e9526c1.png)
- ![image](https://user-images.githubusercontent.com/105793201/233039004-85671b71-9cc0-4717-ba40-b51076c50d34.png)
- Seuraavaksi kirjoitetaan komento **sudo chmod +x hello.sh** , joka antaa oikeudet kaikille käyttäjille ja oikeudet pyörittää ohjelmaa. 
- ![image](https://user-images.githubusercontent.com/105793201/233039366-1108e7d0-60aa-46be-a453-cb7d536468d3.png)
- ongelmia ei ilmennyt joten komento onnistui.
- ![image](https://user-images.githubusercontent.com/105793201/233040201-0da699f3-fb72-4ac1-bef0-f6aa17bcbbb4.png)
- Scripti toimii root kansiossa oletetusti 
- Nyt luodaan path variable **/etc/environment** kansioon PATH eli tiedostopolku, joka löytyy rootista ja siinä on kaikki oikeudet. 
- **PATH="/usr/local/bin/scripts:$PATH"**
- ![image](https://user-images.githubusercontent.com/105793201/233041821-9e5c2909-9296-44bd-9fc2-f614d588a85b.png)
- Refereshataan envronment kansiosto komennolla **source /etc/environment** ja ajetaan komento hello.sh ilman sitä, että olemme root tiedostoissa. 
- ![image](https://user-images.githubusercontent.com/105793201/233042396-6afd4615-a80e-4039-b6ff-80eca95a7c3c.png)
- kaikki toimii oletuksen mukaisesti.
# B) hello.py. Tee oma Python-skripti ja laita se kaikille käyttäjille.

# C) Automatisoi näiden skriptien asennus orjille Saltilla.

# D) Asenna jokin yhden binäärin ohjelma Saltilla orjille.



## References: 
- https://terokarvinen.com/2018/control-windows-with-salt/, Tero Karvinen, 2018
