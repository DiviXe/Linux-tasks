## Git Tehtävät

# Käytössä olevat työkalut:
- Tehtävä tehty windows kympillä Git bashillä.
- tietokoneelle oli asennettu git sivustolta: https://gitforwindows.org/
- ![image](https://user-images.githubusercontent.com/105793201/232413772-6ff742a6-6d53-44aa-83c1-55a8e9c6eecd.png)

# SSH avain luotu aikaisemmin
- SSH avaimen tein aikasemmin tunnilla, valitettavasti siitä luonnista ei ole kuvia. 
- ![image](https://user-images.githubusercontent.com/105793201/232420513-e3cb41b6-13da-4289-897b-440d34dcbcfa.png)


# A) Online. Tee uusi varasto GitHubiin (tai Gitlabiin tai mihin vain vastaavaan palveluun). Varaston nimessä ja lyhyessä kuvauksessa tulee olla sana "summer". Aiemmin tehty varasto ei kelpaa. (Muista tehdä varastoon tiedostoja luomisvaiheessa, esim README.md ja GNU General Public License 3)

- Github varasto luotu missä on readme.md ja GNU General Public License 3
- ![image](https://user-images.githubusercontent.com/105793201/231381623-67b3d60e-e375-468b-8915-46a854a5cb74.png)

# B) Dolly. Kloonaa edellisessä kohdassa tehty uusi varasto itsellesi, tee muutoksia, puske ne palvelimelle, ja näytä, että ne ilmestyvät weppiliittymään.

- Tehtävä pullattu git "kloonamisella" eli **CLONE** ja käytetty SSH:ta sen toteuttamiseen. 
- Tiedosto on vedetty hakemistoon kansioon Git Testi
- ![image](https://user-images.githubusercontent.com/105793201/231382723-3a1cc0f7-656e-44bf-b00f-63e4caa31f83.png)
- Koska kyseessä on windows, teen komennot vähän eri tavalla, mutta periaate on sama (Tottumus kysymys).
- **git init** tarkistetaan että repository on kunnossa ja valmiina komentojen tekemiseen
- ![image](https://user-images.githubusercontent.com/105793201/231383050-fd365255-04c1-4442-b801-d6873ff36918.png)
- **nano readme.md** muutetaan tiedoston sisältöä 
- ![image](https://user-images.githubusercontent.com/105793201/231383560-19462def-b736-48af-8c08-6a9d31f5edaa.png)
- ![image](https://user-images.githubusercontent.com/105793201/231383643-b3651c92-ed3a-4367-9b88-0bf731f3fcb9.png)
- Nyt ajetaan komento **git pull** varmuuden vuoksi, ettei välissä ole tullut mitään muita muutoksia. 
- ![image](https://user-images.githubusercontent.com/105793201/231384032-4f5ff6f1-64f7-42ec-b0ac-d0c9ee929d54.png)
- "Already up to date" eli tiedosto on jo ajantasalla.
- Tehdään komento **git add .**, piste meinaa sitä, että annetaan mennä läpi kaikki muutokset jota koko kansioon on tehty. 
- ![image](https://user-images.githubusercontent.com/105793201/231384333-e32a9e74-fb79-45ce-bf08-c8f4edb585a9.png)
- Tehdään **"git commit -m "tekstiä"** -m tarkoittaa, että commit teksti tulee main branchiiin ja tämän jälken voimme kirjoittaa viestin. 
- ![image](https://user-images.githubusercontent.com/105793201/231384692-f0c2b2d7-feee-4659-9697-62ea64d77086.png)
- Kokeillaan seuraavaksi **"git push -u origin main"** eli pusketaan muutokset itse repositoryyn, joka on gitissä.
- ![image](https://user-images.githubusercontent.com/105793201/231385131-15eb1112-59db-497e-a055-3b95190ea6f0.png)
- Näytti toimivan! Katsotaan vielä muutokset gitissä.
- ![image](https://user-images.githubusercontent.com/105793201/231385235-dc6114f7-52c2-4ca9-a04e-113cdde1ceae.png)
- ![image](https://user-images.githubusercontent.com/105793201/231385335-4eba8fd2-7b3b-421e-97af-169ef8f95f83.png)
- Kommentti näkyy ja tiedostokin on muuttunut

# C) Doh! Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset --hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.
- ![image](https://user-images.githubusercontent.com/105793201/231402181-b3d4d988-6c7b-4e40-b73c-95bf8ba0d6b7.png)
- Oho nyt tuli tyhmiä muutoksia! Tehdään **reset --hard**, tuodaan vanha pusku läpi.
- ![image](https://user-images.githubusercontent.com/105793201/231402282-34155efd-f29f-4b25-ba19-6ad7ac503dca.png)
- ![image](https://user-images.githubusercontent.com/105793201/231402376-62006ab5-de6e-40e1-8b84-3e2d675e5e14.png)
- Readme.md on nyt palautunut normaaliiksi!
-
# D) Tukki. Tarkastele ja selitä varastosi lokia. Tarkista, että nimesi ja sähköpostiosoitteesi näkyy haluamallasi tavalla ja korjaa tarvittaessa.
- katsotaan logitiedostoja Githubista komennolla **git log --patch**
- ![image](https://user-images.githubusercontent.com/105793201/231430723-334773ea-5082-485d-9958-525a1ba680bd.png)
- pistin sähköposti osoitteen piiloon. Tässä näkyy, että olen Leo Ahopalo käyttäjällä tehnyt yhden commitin
- Olen lisännyt tekstitiedostoon readme.md +hei pukki älä tule vielä, koska kesä tulee :)
- DiviXe github käyttäjä on myös mukana
- Siinä kaikki harjoitus on valmis.

## References
- https://terokarvinen.com/2023/palvelinten-hallinta-2023-kevat/, Tero karvinen
