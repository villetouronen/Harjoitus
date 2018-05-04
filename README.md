# Harjoitus
Palvelin hallinta harjoitus 5 - Oma moduuli ja oma git-varasto

Tämä on raporttini tämän viikon harjoituksesta, joka on osa Tero Karvisen
Palvelinten Hallinta-kurssin tehtäviä. [Tässä linkki tehtäviin.](http://terokarvinen.com/2018/aikataulu-%E2%80%93-palvelinten-hallinta-ict4tn022-4-ti-5-ke-5-loppukevat-2018-5p#h5)

Harjoituksessa käyttämäni kone on MSI:n GX 640 (64-bit) kannettava tietokone
ja koneeseen on asennettu käyttöjärjestelmäksi Linux Xubuntu 16.04.3 LTS (64-bit).

Teen nämä harjoitukset aiemmin luomallani live-tikulla. Voit saada oman Xubuntu
16.04.3 LTS (64-bit) versiosi [täältä.](http://torrent.ubuntu.com/xubuntu/releases/xenial/release/desktop/xubuntu-16.04.4-desktop-amd64.iso.torrent)

## Valmistelu

Koska tehtävissä käytetään Saltia ja Gitiä, ne tarvitsee asentaa ennen muita
tehtäviä asioita. Mutta muistetaan kuitenkin tehdä muutama muu asia ennen tätä,
koska kyseessä on live-tikku.

	$ setxkbmap fi
	$ sudo apt-get update
	$ sudo apt-get -y install git salt-minion

## a) Valitse aihe omaksi kurssityöksi ja varaa se kommenttina aikataulusivun 
perään.

Oma aiheeni on Logstashin asennus ja sen konfigurointi. Tällä ohjelmalla voidaan
kerätä dataa eri lähteistä ja yhdistää ne yhteen luettavaan muotoon. Tavoitteena
on saada toimiva sovellus analyysiä ja monitorointia varten omaan käyttöön.

## b) Julkaise raportti MarkDownilla. Jos käytät GitHub:ia, se tekee muotoilun 
automaattisesti “.md”-päätteisiin dokumentteihin.

Aloitin tämän kohdan luomalla repositoryn Githubissa. Loin samalla myös tuonne 
repositoryyn valmiiksi mukaan README.md-tiedoston. Tämän jälkeen kloonasin sen
harjoituksessa käyttämälleni kannettavalla tietokoneelle seuraavalla komennolla.

	$ git clone https://github.com/villetouronen/Harjoitus5.git

Tuota samalla luomaamme pääsemme muokkaamaan ja kirjoittamaan sinne raporttimme 
tästä harjoituksesta seuraavilla komennoilla.

	$ cd Harjoitus5
	$ nano README.md

Ohjeita MarkDownin tekstin muotoilua varten löydät [täältä.](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

Seuraavaksi voit avata uuden välilehden terminaaliin, jotta pääset luomaan omaa
Salt-tilaa.

##c) Aja oma Salt-tila suoraa git-varastosta. Voit joko tehdä tilan alusta lähtien 
itse tai forkata sirottimen. 

Aloitetaan luomalla ensin top.sls-tiedosto samaan repositoryyn. Tämä onnistuu seuraavalla
komennolla.

	$ nano top.sls

[Tiedoston sisältö näyttää kutakuinkin tältä.](https://github.com/villetouronen/Harjoitus5/top.sls)

Tämän jälkeen voimme luoda install.sls-tiedoston samaan repositoryyn, joka määrittelee 
asennettavat ohjelmat. Tämä onnistuu seuraavalla komennolla.

	$ nano install.sls

[Tiedoston tulisi näyttää tältä.](https://github.com/villetouronen/Harjoitus5/install.sls)


