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
- 




# A) Asenna Debian 11 Vagrantilla.
- Debian ladattu onnistuneesti VM boxiin. 
![image](https://user-images.githubusercontent.com/105793201/228643756-3686698a-0981-4bf9-b954-a3d44c23ec38.png)


# B) 



 ## References
 
 Karvinen 2023: https://terokarvinen.com/2023/create-a-web-page-using-github/, 
 https://terokarvinen.com/2020/command-line-basics-revisited/, 
 https://terokarvinen.com/2023/salt-vagrant/
