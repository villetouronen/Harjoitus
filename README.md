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

## a) Valitse aihe omaksi kurssityöksi ja varaa se kommenttina aikataulusivun perään.

Oma aiheeni on Logstashin asennus ja sen konfigurointi. Tällä ohjelmalla voidaan
kerätä dataa eri lähteistä ja yhdistää ne yhteen luettavaan muotoon. Tavoitteena
on saada toimiva sovellus analyysiä ja monitorointia varten omaan käyttöön.

## b) Julkaise raportti MarkDownilla. Jos käytät GitHub:ia, se tekee muotoilun automaattisesti “.md”-päätteisiin dokumentteihin.

Aloitin tämän kohdan luomalla repositoryn Githubissa. [Löydät ohjeet tähän tältä sivulta.](http://terokarvinen.com/2016/publish-your-project-with-github) 
Loin samalla myös tuonne repositoryyn valmiiksi mukaan README.md-tiedoston. Tämän jälkeen kloonasin sen
harjoituksessa käyttämälleni kannettavalla tietokoneelle seuraavalla komennolla.

	$ git clone https://github.com/villetouronen/Harjoitus5.git

Tuota samalla luomaamme pääsemme muokkaamaan ja kirjoittamaan sinne raporttimme 
tästä harjoituksesta seuraavilla komennoilla.

	$ cd Harjoitus5
	$ nano README.md

Ohjeita MarkDownin tekstin muotoilua varten löydät [täältä.](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

Seuraavaksi voit avata uuden välilehden terminaaliin, jotta pääset luomaan omaa
Salt-tilaa.

## c) Aja oma Salt-tila suoraa git-varastosta. Voit joko tehdä tilan alusta lähtien 
itse tai forkata sirottimen. 

Aloitetaan luomalla ensin top.sls-tiedosto samaan repositoryyn. Tämä onnistuu seuraavalla
komennolla.

	$ nano top.sls

[Tiedoston sisältö näyttää kutakuinkin tältä.](https://github.com/villetouronen/Harjoitus5/top.sls)

Tämän jälkeen voimme luoda install.sls-tiedoston samaan repositoryyn, joka määrittelee 
asennettavat ohjelmat. Tämä onnistuu seuraavalla komennolla.

	$ nano install.sls

[Tiedoston tulisi näyttää tältä.](https://github.com/villetouronen/Harjoitus5/install.sls)

Koska loimme top.sls-tiedoston meidän ei tarvitse asentaa Salt masteria ja konfiguroida sitä. Voimme 
siis ajaa suoraan tilan seuraavalla komennolla.

	$ sudo salt-call -- local state.highstate --file.root .

Tämän jälkeen voimme committaa ja siirtää kaiken tavaran githubiin seuraavalla komennolla.

	$ git add . && git commit; git pull && git push

Onneksi olkoon! Nyt kaikki on siirretty githubin suojiin, josta voit ajaa ne aina tarvittaessa.
Seuraavaksi voimme poistaa hakemiston ja ohjelmat jotka on koneellasi, kloonata sen uudelleen ja lopulta
ajaa uudelleen tuon tilan. Tämä onnistuu seuraavilla komennoilla.

	$ rm -rf Harjoitus5
	$ sudo apt-get purge -y vlc cmatrix figlet
	$ git clone https://github.com/villetouronen/Harjoitus5.git
	$ cd Harjoitus5
	$ sudo salt-call -- local state.highstate --file.root .

Terminaali tulosti seuraavan näkymän:

	local:
	----------
        	ID: install_test
    		Function: pkg.installed
      		Result: True
     		Comment: 3 targeted packages were installed/updated.
     		Started: 10:44:47.620361
    		Duration: 31835.868 ms
     	Changes:   
              ----------
              cmatrix:
                  ----------
                  new:
                      1.2a-5build2
                  old:
              figlet:
                  ----------
                  new:
                      2.2.5-2
                  old:
              liba52-0.7.4:
                  ----------
                  new:
                      0.7.4-18
                  old:
              libbasicusageenvironment1:
                  ----------
                  new:
                      2016.02.09-1
                  old:
              libcddb2:
                  ----------
                  new:
                      1.3.2-5fakesync1
                  old:
              libchromaprint0:
                  ----------
                  new:
                      1.3-1
                  old:
              libdc1394-22:
                  ----------
                  new:
                      2.2.4-1
                  old:
              libdca0:
                  ----------
                  new:
                      0.0.5-7build1
                  old:
              libdirectfb-1.2-9:
                  ----------
                  new:
                      1.2.10.0-5.1
                  old:
              libdvbpsi10:
                  ----------
                  new:
                      1.3.0-4
                  old:
              libdvdnav4:
                  ----------
                  new:
                      5.0.3-1
                  old:
              libdvdread4:
                  ----------
                  new:
                      5.0.3-1
                  old:
              libebml4v5:
                  ----------
                  new:
                      1.3.3-1
                  old:
              libfaad2:
                  ----------
                  new:
                      2.8.0~cvs20150510-1
                  old:
              libfreerdp-cache1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-client1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-codec1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-common1.1.0:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-core1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-crypto1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-gdi1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-locale1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-primitives1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libfreerdp-utils1.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libgl1-mesa-glx:
                  ----------
                  new:
                      17.2.8-0ubuntu0~16.04.1
                  old:
                      17.0.7-0ubuntu0.16.04.1
              libglapi-mesa:
                  ----------
                  new:
                      17.2.8-0ubuntu0~16.04.1
                  old:
                      17.0.7-0ubuntu0.16.04.1
              libgles2:
                  ----------
                  new:
                      1
                  old:
              libgles2-mesa:
                  ----------
                  new:
                      17.2.8-0ubuntu0~16.04.1
                  old:
              libgroupsock8:
                  ----------
                  new:
                      2016.02.09-1
                  old:
              libiso9660-8:
                  ----------
                  new:
                      0.83-4.2ubuntu1
                  old:
              libkate1:
                  ----------
                  new:
                      0.4.1-7
                  old:
              liblircclient0:
                  ----------
                  new:
                      0.9.0-0ubuntu6
                  old:
              liblivemedia50:
                  ----------
                  new:
                      2016.02.09-1
                  old:
              liblua5.2-0:
                  ----------
                  new:
                      5.2.4-1ubuntu1
                  old:
              libmad0:
                  ----------
                  new:
                      0.15.1b-8ubuntu1
                  old:
              libmatroska6v5:
                  ----------
                  new:
                      1.4.4-1
                  old:
              libmpcdec6:
                  ----------
                  new:
                      2:0.1~r459-4.1build1
                  old:
              libmpeg2-4:
                  ----------
                  new:
                      0.5.1-7
                  old:
              libpcre16-3:
                  ----------
                  new:
                      2:8.38-3.1
                  old:
              libproxy-tools:
                  ----------
                  new:
                      0.4.11-5ubuntu1
                  old:
              libqt5core5a:
                  ----------
                  new:
                      5.5.1+dfsg-16ubuntu7.5
                  old:
              libqt5dbus5:
                  ----------
                  new:
                      5.5.1+dfsg-16ubuntu7.5
                  old:
              libqt5gui5:
                  ----------
                  new:
                      5.5.1+dfsg-16ubuntu7.5
                  old:
              libqt5network5:
                  ----------
                  new:
                      5.5.1+dfsg-16ubuntu7.5
                  old:
              libqt5svg5:
                  ----------
                  new:
                      5.5.1-2build1
                  old:
              libqt5widgets5:
                  ----------
                  new:
                      5.5.1+dfsg-16ubuntu7.5
                  old:
              libqt5x11extras5:
                  ----------
                  new:
                      5.5.1-3build1
                  old:
              libresid-builder0c2a:
                  ----------
                  new:
                      2.1.1-14ubuntu2
                  old:
              libsdl-image1.2:
                  ----------
                  new:
                      1.2.12-5+deb9u1build0.16.04.1
                  old:
              libsdl1.2debian:
                  ----------
                  new:
                      1.2.15+dfsg1-3
                  old:
              libsidplay2v5:
                  ----------
                  new:
                      2.1.1-14ubuntu2
                  old:
              libssh2-1:
                  ----------
                  new:
                      1.5.0-2ubuntu0.1
                  old:
              libupnp6:
                  ----------
                  new:
                      1:1.6.19+git20160116-1
                  old:
              libusageenvironment3:
                  ----------
                  new:
                      2016.02.09-1
                  old:
              libva-drm1:
                  ----------
                  new:
                      1.7.0-1ubuntu0.1
                  old:
              libva-x11-1:
                  ----------
                  new:
                      1.7.0-1ubuntu0.1
                  old:
              libvcdinfo0:
                  ----------
                  new:
                      0.7.24+dfsg-0.2
                  old:
              libvlc5:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              libvlccore8:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              libvncclient1:
                  ----------
                  new:
                      0.9.10+dfsg-3ubuntu0.16.04.2
                  old:
              libwinpr-crt0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-dsparse0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-environment0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-file0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-handle0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-heap0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-input0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-interlocked0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-library0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-path0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-pool0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-registry0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-rpc0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-sspi0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-synch0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-sysinfo0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-thread0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libwinpr-utils0.1:
                  ----------
                  new:
                      1.1.0~git20140921.1.440916e+dfsg1-5ubuntu1.2
                  old:
              libxcb-composite0:
                  ----------
                  new:
                      1.11.1-1ubuntu1
                  old:
              libxcb-icccm4:
                  ----------
                  new:
                      0.4.1-1ubuntu1
                  old:
              libxcb-image0:
                  ----------
                  new:
                      0.4.0-1build1
                  old:
              libxcb-keysyms1:
                  ----------
                  new:
                      0.4.0-1
                  old:
              libxcb-randr0:
                  ----------
                  new:
                      1.11.1-1ubuntu1
                  old:
              libxcb-render-util0:
                  ----------
                  new:
                      0.3.9-1
                  old:
              libxcb-xkb1:
                  ----------
                  new:
                      1.11.1-1ubuntu1
                  old:
              libxcb-xv0:
                  ----------
                  new:
                      1.11.1-1ubuntu1
                  old:
              libxkbcommon-x11-0:
                  ----------
                  new:
                      0.5.0-1ubuntu2
                  old:
              mp3-decoder:
                  ----------
                  new:
                      1
                  old:
              qtbase-abi-5-5-1:
                  ----------
                  new:
                      1
                  old:
              qtsvg-abi-5-4-0:
                  ----------
                  new:
                      1
                  old:
              qttranslations5-l10n:
                  ----------
                  new:
                      5.5.1-2build1
                  old:
              vlc:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              vlc-data:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              vlc-nox:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              vlc-plugin-notify:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:
              vlc-plugin-samba:
                  ----------
                  new:
                      2.2.2-5ubuntu0.16.04.4
                  old:

	Summary for local
	------------
	Succeeded: 1 (changed=1)
	Failed:    0
	------------
	Total states run:     1

Tilan ajo meni läpi. Seuraavaksi kokeillaan ohjelmat.

[Täältä löydät kuvan ohjelmien testistä.](https://haagahelia-my.sharepoint.com/:i:/g/personal/a1700401_myy_haaga-helia_fi/ERGFdU2sFBNIt5X3RoDulXYB42HXZ3y7IpFYDfc2cIYEQQ?e=MaGfbE)

Ohjelmat toimivat!
	

