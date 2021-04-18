# H3 Versionhallinta

## Tehtävä A
> a) MarkDown. Tee tämän tehtävän raportti MarkDownina. Helpointa on tehdä raportti GitHub-varastoon, jolloin md-päätteiset
> tiedostot muotoillaan automaattisesti. Tyhjä rivi tekee kappalejaon, risuaita ‘#’ tekee otsikon, sisennys merkitsee koodinpätkän.
> Vinkkinä artikkelini Publish Your Project with GitHub.  
[TeroKarvinen.com](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/)

### GitHub
GitHub tili on tehty aikasemmin sen tuomien GitHub Education etujen takia  
[https://education.github.com/](https://education.github.com/).  
Aloitetaan tekemällä uusi repositio valitsemalla kirjautumisen jälkeen "New" vasemmasta ylälaidasta.  

![uusi repositio](/pic/github.JPG)

Seuraavaksi annetaan repositiolle nimi, lyhyt tekstit joka selittää mikä sen tarkoitus on, lisätään README.md tiedosto valmiiksi
 ja annetaan lisenssioikeudet.  

![reposition tiedot](/pic/github1.JPG)  

Ja näin meillä on uusi repositio luotuna

### Repositorion cloonaus
Ensin asennetan git  
`$ sudo apt-get update`  
`$ sudo apt-get -y install git`  

Kerrotaan gitille kuka me olemme, tämä tieto kirjautuu aina tehtyjen muutosten mukana tiedostoon  
`$ git config --global user.email "lindellgit@gmx.com"`  
`$ git config --global user.name "Johan Lindell"`  

Kopioidaan tämä uusi repositorio tietokoneelle, osoite saadaan reposition etusivulta, "CODE" kohdasta  

![repositio valmis](/pic/github2.JPG)  

`$ git clone https://github.com/johanlindellgit/githubharkka.git` 

Näin meillä on tiedostot koneella ja voimme aloittaa niiden käytön.  

![git clone](/pic/github3.JPG)  

---
## Tehtävä B
> d) Näytä omalla git-varastollasi esimerkit komennoista ‘git log’, ‘git diff’ ja ‘git blame’. Selitä tulokset.  
[TeroKarvinen.com](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/)

### Git log
`git log`  
Tällä käskyllä näemme viimeaikaiset lisäykset repositorioon, tästä näemme esimerkiksi että Johan Lindell on korjannut
kirjoitusvirheitä ja ulkoasua, mutta koska ei ole committiin kirjoittanut että missä tiedostossa niin se jää hieman auki.

![git log](/pic/gitlog.JPG)

### Git blame
Tällä käskyllä näemme tiedostosta kuka on kirjoittanut minkäkin rivin ja koska, kirjoitusvirheiden tekijästä ei jää epäilystä.  
`git blame H3Versionhallinta.md`  

![git blame](/pic/gitblame.JPG)

---
## Tehtävä E
> e) Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset –hard’. Huomaa, että tässä
> toiminnossa ei ole peruutusnappia.  
[TeroKarvinen.com](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/)

Muutetaan H3Versionhallinta.md tiedostoa. Muutokset olikin hölmöjä, joten palataan takaisin githubin viimeisimpään versioon
 tuosta tiedostosta komennolla  
`git reset --hard`  
Tiedostot on nyt palautettu ja muutokset tuhottu
![git hard reset](/pic/gitreset.JPG)

---
## Tehtävä F
> f) Tee uusi salt-moduli. Voit asentaa ja konfiguroida minkä vain uuden ohjelman: demonin, työpöytäohjelman tai komentokehotteesta 
> toimivan ohjelman. Käytä tarvittaessa ‘find -printf “%T+ %p\n”|sort’ löytääksesi uudet asetustiedostot. (Tietysti eri ohjelma kuin
> aiemmissa tehtävissä, tarkoitushan on harjoitella Salttia)  
[TeroKarvinen.com](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-spring-2021/)

## Git
Asensimme juuri gitin käsin, joten asennetaan sen nyt saltin avulla, lisätään siihen myös
 komentona omien tietojen lisäys ja komento pysyä kirjautuneena hieman pidempään.  
Aloitetaan kuten aina salt kansion sisään oma kansio tälle moduulille ja sen sisään inti.sls tiedosto. 
Ensin tehdään "hello world" testi, jotta voidan varmistua että ohjelma toimii halutulla tavalla. Tämän jälkeen muutetaan 
init.sls tiedostoa ja lisätään sinne komento asentaa git.  
`git:  

  pkg.installed`  
Testataan tämän toiminta.  
`$ sudo salt '*' state.apply tehtava3`  

![git asennus](/pic/gitinstall.JPG)  

Lisätän init.sls tiedostoon komennot tallentaa nimi, sähköpostiosoite ja muutetaan aikakatkaisua, näin
ei tarvitse kirjoittaa salasanaa joka push komennon yhteydessä.

`'git config --system user.email "lindellgit@gmx.com"; git config --system user.name "Johan Lindell"; git config --system credential.helper "cache --timeout=3600"':  
  cmd.run`

![git asennus](/pic/gitsalt.JPG) 

komennolla `$ sudo find -printf "%T+ %p\n"|sort` näemme että tiedostoon nimeltä gitconfig on tullut
muutoksia, katsotaan mitä se sisältää.

![git asennus](/pic/gitconfig.JPG)

Juuri ne muutokset jotka komennolla teimme.
