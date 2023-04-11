# H2 Demonit

## X) Lue ja tiivistä Pkg-File-Service-Control Daemons with Salt – Change SSH Server Port .

- Tavoitteet:
- Asenna ohjelmisto, vaihda asetustitiedosto ja lopuksi käynnistä demoni uudelleen käyttääksesi uutta kokoonpanoa (Tässä tilanteessa porttia). 
- Artikeli kertoo yksinkertiasen saltstaten SSh-palvelin portin muuttamiseksi
- master käyttäjällä luodaan state (sshd.sls) ja määritystiedoston pääkopio (sshd_config). 
- tehdään komento **$ cat /srv/salt/sshd.sls** ja laitetaan paketit kuntoon. 
- vaihdetaan #port22 portiksi 8888 ja tallenetaan tiedosto.
- tallennetaan muutokset **$ sudo salt '*' state.apply sshd**
- testataan toimivuutta esimerkiksi **$ $ ssh -p 8888 tero@tero.example.com**
- tämän jälkeen sinun pitäisi päästä koneellesi!

## A) Asenna OpenSSH-palvelin käsin
- Ensin ajoin komennon **sudo passwd vagrant**
- Annettin uusi salasana
- Kirjauduttiin VirtualBoxilla virtuaalikoneen "t001" komentokehotteella sisään
- Tämän jälkeen poistin t001 virtuaalikoneen openssh:n komennolla **sudo apt purge openssh-server**
- käynnistin koneen uudestaan
- ja perään asensin sen uudestaan komennolla **sudo apt install openssh-server**
- ![image](https://user-images.githubusercontent.com/105793201/230332776-e829e58b-fb4a-43e8-8c10-256d261cd81b.png)
- yritin katsoa manuualista miten portti vaihdetaan ja kokeilin komentoa **sudo sshd -p 8888**, mutta se ei toiminut.
- menin sitten ssh tiedostoon **nano/etc/ssh/sshd config** ja muutin portiksi 8888. 
- ![image](https://user-images.githubusercontent.com/105793201/230333864-473afefa-b115-4ff9-be4e-30105a3e3f27.png)
-	Tämän jälkeen uudelleen käynnistän SSH demonin komennolla **sudo systemctl restart sshd**
- Testasin, että mikä meininki on ssh:ssä komennolla sudo systemctl status ssh ja port 8888 näyttää olevan auki. 
- ![image](https://user-images.githubusercontent.com/105793201/230335015-3e4b0aeb-d3b4-4774-8c30-ada936afce30.png)
- testataan windowsilla saadaanko yhteys!
- Pingaus t001 virtuaalikoneeseen ainakin toimii.
- ![image](https://user-images.githubusercontent.com/105793201/230335224-34cebaf0-2c6e-4a51-94b4-c935bcf882bb.png)
- kokeillaan ssh (virtuaaliyhteys) komennolla **ssh-p 8888 vagrant@192.168.12.100**
- sisälle päästiin!
- ![image](https://user-images.githubusercontent.com/105793201/230335449-0dd06f43-c2a8-49c0-b2c9-9aaefb508b73.png)

## B) Automatisoi äsken tekemäsi SSH-konfiguraatio Saltilla.
- Hypätään takaisin master käyttäjälle komennolla **exit**
- tämän jälkeen otetaan yhteys masteriin komennolla **vagrant ssh tmaster**
- ![image](https://user-images.githubusercontent.com/105793201/230591855-66da64ef-405b-4f39-96c0-46be843f7598.png)
- luodaan uusikansio salttiin komennolla **sudo mkdir -p /srv/salt/**
- mennään sen luo komennolla **cd /srv/salt**
- ![image](https://user-images.githubusercontent.com/105793201/230592232-ea05a878-a869-4cab-bb1d-1d870804aed0.png)
- editoidaan tiedostoa, liitetään SSH state (tila) ja kopiodaan Tero Karvisen koodi.
- **sudoedit sshd.sls**
- ![image](https://user-images.githubusercontent.com/105793201/230592371-a2d2fc02-14d9-4283-b6dd-74f19cc99b9d.png)
- mennään takaisin hakemistoon /etc/ssh komennolla **cd /etc/ssh**
- muutetaan ssh.configin porttia samaksi, mikä t001 koneella oli eli 8888 
- ![image](https://user-images.githubusercontent.com/105793201/230593896-254659f8-3c8d-4e88-a498-46c4720e3340.png)
- kokeillaan save tuli error viesti no minions matched the target. 
- ![image](https://user-images.githubusercontent.com/105793201/230593972-75ba0974-41d3-4a5d-b21b-17c943a1f34d.png)
- ongelmana oli, että en ollut hyväksynyt salt keytä t001 ja t002. 
- ![image](https://user-images.githubusercontent.com/105793201/230793363-edbffc6b-68c6-4738-a54c-9b1e2c1148c3.png)
- Lisää ongelmia: 
- ![image](https://user-images.githubusercontent.com/105793201/230793499-92c134da-c2be-4ff2-981c-c878d0593db6.png)
- Ongelmana oli, että srv/salt kansiossa ei ole sshd_config tiedostoa, joten lähdin luomaan kyseistä kansiota
- ![image](https://user-images.githubusercontent.com/105793201/230793711-3b9b64d8-1897-42c6-9fee-f7b057b12635.png)
- tein prosessin uudestaan varmuuden vuoksi, 
- Luotiin kansio srv/salt{files,states} komennolla **sudo mkdir -p /srv/salt/{files,states}**
- Luotiin lisäkansio sshd ja kapioidaan sshd_config ssh fileistä srv/salttiin **sudo cp /etc/ssh/sshd_config /srv/salt/files/sshd/**
- Katsottiin yhteensopivuus komennolla sudo **chmod 644 /srv/salt/files/sshd/sshd_config**
- Tämän jälkeen katsottiin, että tiedosto oikeasti on siellä ja muokattiin tiedosto samanlaiseksi kuin edellisissä kuvissa. 
- **$ sudo ls /srv/salt/**
- **$ sudo salt '*' state.apply sshd** tallennuksen jälkeen muille virtuaalikoneille muutos onnistui!
- ![image](https://user-images.githubusercontent.com/105793201/230793872-c77d6f87-9c5c-4f6f-85df-5254dfa0d609.png)
- ![image](https://user-images.githubusercontent.com/105793201/230793878-90cd84e3-b32d-497f-9cbb-91313071e5c6.png)
- Kokeillaan idempotenttisuus.
- ![image](https://user-images.githubusercontent.com/105793201/230793890-bc4972ac-01fa-41ae-bb66-b57c9b86925b.png)
- Mikään ei enään muuttunut (mikä on hyvä)
- Kokeillaan yhteys seuraavaksi.
- Katsotaan T001 tietokoneiden IP osoitteet testiä varten.
- ![image](https://user-images.githubusercontent.com/105793201/230793992-b57f9c2f-257b-4442-9f8a-200f1c4dcaf8.png)
- Testataan yhteys koneeseen t001 komennolla **$ ssh -p 8888 vagrant@192.168.12.100**
- ![image](https://user-images.githubusercontent.com/105793201/230794446-ca7d2c97-0954-43b6-af6f-0ae1d3e4e29a.png)
- Sisään päästiin!
## C) Tee jokin muu asetus äsken tekemääsi SSH-palveluun. Osoita testein, että Salt käynnistää demonin uudelleen, kun asetustiedosto on muuttunut (jolloin uudet asetukset tulevat voimaan).
- Ajattelin lisätä kolmannen portin tmasterin sshd_config tiedostoon mikä on salt kansiossa ja katsoa mitä tapahtuu kun komento **$ sudo salt '*' state.apply sshd** tehdään uudestaan.
- ![image](https://user-images.githubusercontent.com/105793201/230852638-a0de2bf2-b202-440f-904f-360b6528c607.png)
- Portti 1255 tuli käyttöön (ensiksi ajattelin nimeä 1234, mutta muutin nimen 1255) 
- ![image](https://user-images.githubusercontent.com/105793201/230853277-ed7656fc-0fed-4b5e-8b18-f1f5d33565db.png)
- ![image](https://user-images.githubusercontent.com/105793201/230853316-55234a6b-89bf-4fca-be38-b080db0df84c.png)
- SSH service on tämän jälkeen uudelleen käynnistetty. 
- Ajetaampas komento uudestaan ilman tekemättä muutoksia.
- ![image](https://user-images.githubusercontent.com/105793201/230853561-2488e308-57b1-4556-b242-ef39c6b0ae31.png)
- kommentiksi tulee, että the service sshd is already running eli vain jos sshd_config tiedostoa muutetaan niin sshd palvelin uudelleenkäynnistyy.
-  Kokeillaan portin toimivuus
-  ![image](https://user-images.githubusercontent.com/105793201/230854141-d07ef9ed-5a20-422e-a39e-0706d36aa06a.png)
-  Yhteyttä ei saatu yhdistettyä, kokeillaan vaihtaa palomuurin asetuksia, (kyseessä olikin väärä IP-osoite).
-  ![image](https://user-images.githubusercontent.com/105793201/230855073-ad693ca1-d11f-49b7-8d82-0463ab7ce4c8.png)
- sisälle päästiin!


# References:
- https://terokarvinen.com/2023/palvelinten-hallinta-2023-kevat/, Tero karvinen
- https://terokarvinen.com/2018/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/?fromSearch=salt%20ssh, Tero karvinen
- 

