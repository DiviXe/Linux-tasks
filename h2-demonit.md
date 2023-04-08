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

- tein tämän omalla tavalla siten, että resetoin salasanan koneelle "t001" komennolla **sudo passwd**
- tämän jälkeen kirjauduin virtuaalikoneeseen t001 virtualboxin kautta poistin openssh:n komennolla **sudo apt purge openssh-server**
- käynnistin koneen uudestaan komennolla **shutdown**
- ja perään asensin sen uudestaan komennolla **sudo apt install openssh-server**
- ![image](https://user-images.githubusercontent.com/105793201/230332776-e829e58b-fb4a-43e8-8c10-256d261cd81b.png)
- yritin katsoa manuualista miten portti vaihdetaan ja kokeilin komentoa **sudo sshd -p 8888**, mutta se ei toiminut.
- menin sitten ssh tiedostoon **nano/etc/ssh/sshd config** ja muutin portiksi 8888. 
- ![image](https://user-images.githubusercontent.com/105793201/230333864-473afefa-b115-4ff9-be4e-30105a3e3f27.png)
-	Tämän jälkeen uudelleen käynnistän SSH demonin komennolla **sudo systemctl restart sshd**
- Testasin, että mikä meininki on ssh:ssä komennolla sudo systemctl status ssh ja port 8888 näyttää olevan auki. 
- ![image](https://user-images.githubusercontent.com/105793201/230335015-3e4b0aeb-d3b4-4774-8c30-ada936afce30.png)
- testataan windowsilla saadaanko yhteys!
- Pingaus f001 virtuaalikoneeseen ainakin toimii.
- ![image](https://user-images.githubusercontent.com/105793201/230335224-34cebaf0-2c6e-4a51-94b4-c935bcf882bb.png)
- kokeillaan ssh (virtuaaliyhteys) komennolla **-p 8888 vagrant@192.168.12.100**
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
- muutetaan ssh.configin porttia samaksi, mikä f001 koneella oli eli 8888 
- ![image](https://user-images.githubusercontent.com/105793201/230593896-254659f8-3c8d-4e88-a498-46c4720e3340.png)
- kokeillaan save tuli error viesti no minions matched the target. 
- ![image](https://user-images.githubusercontent.com/105793201/230593972-75ba0974-41d3-4a5d-b21b-17c943a1f34d.png)


