# H2 Demonit

## X) Lue ja tiivistä Pkg-File-Service-Control Daemons with Salt – Change SSH Server Port .

- Tavoitteet:
- Asenna ohjelmisto, vaihda asetustitiedosto ja lopuksi käynnistä demoni uudelleen käyttääksesi uutta kokoonpanoa (Tässä tilanteessa porttia). 
- Artikeli kertoo yksinkertiasen saltstaten SSh-palvelin portin muuttamiseksi
- master käyttäjällä luodaan state (sshd.sls) ja määritystiedoston pääkopio (sshd_config). 
- tehdään komento ** $ cat /srv/salt/sshd.sls** ja laitetaan paketit kuntoon. 
- vaihdetaan #port22 portiksi 8888 ja tallenetaan tiedosto.
- tallennetaan muutokset **$ sudo salt '*' state.apply sshd**
- testataan toimivuutta esimerkiksi **$ $ ssh -p 8888 tero@tero.example.com**
- tämän jälkeen sinun pitäisi päästä koneellesi!



