# Go

Go-kielellä on muutamia erikoisuuksia, jotka saattavat hämmentää Java-kirjoittajaa. Tämän artikkelin tarkoitus on avittaa muita pääsemään helpommin ja nopeammin sinuiksi Go:hon, jotta itse arvointi ja koodinkatselmus olisi helpompaa.


## Go:n asentaminen

Jos käyttöjärjestelmäsi on Linux voit todennäköisesti asentaa Go:n pakettihallintajärjestelmän kautta. Katso ohjeet kuinka asennus tapahtuu omassa linux-ympäristössäsi. MacOS käyttäjien kannattanee asentaa Go [homebrewin](https://brew.sh/) kautta.

Muille käyttöjärjestelmille tai manuaalisesta asennuksesta kiinnostuneille kannatta katsoa [Go:n omista dokumenteista](https://golang.org/doc/install).


### GOPATH muuttujan asettaminen

Ympäristömuuttuja `GOPATH` kertoo minne Go asentaa ohjelmansa ja riippuvuutensa. Itselläni `GOPATH` on asetettu `.zshrc` tiedostossa kotikansiossa. `.bashrc` on myös toinen paikka, minne kannattanee asettaa muuttuja, jos shell on bash (jos järjestelmään ei ole tehty mitään muutoksia, on shellinä todennäköisesti bash). Seuraava koodirivi asettaa `GOPATH` muuttujan:

```sh
export GOPATH="${HOME}/Code/go"
```

Jotta Go:n binäärit voisia ajaa helposti, kannattaa laittaa viimeiseksi koodiriviksi seuraava:

```sh
export PATH="$PATH:${GOPATH}/bin"
```


## TiraLabraRegex ohjelman asentaminen ja käyttö

Kun Go on asennettuna, voidaan TiraLabraRegex asentaa seuraavasti:

```sh
go get -v github.com/Gredu/TiraLabraRegex
```

Käyttäminen tapahtuu siten, että ensimmäisenä parametrina on tiedosto, joka sisältää sanoja. Toinen parametri (stringinä) on säännöllinen lauseke, johon tiedoston sanat käydään läpi. Jos sana sopii säännölliseen lausekkeeseen, se tulostetaan. Esimerkiksi:

```sh
TiraLabraRegex data/inputs "jaava"
```


## Tiedostorakenne

Muista kielistä on tuttu nimitys "workspace" (suom. työalue), jolla tarkoitetaan työaluetta, joka käytännössä sisältää kaiken, mitä yhdessä projektissa on. Työalue sisältää yleensä mm. kansion binääreille, paketeille ja lähdekoodeille. Erikseen saattaa olla myös projektiin liittyvät konfiguraatio tiedostot ja kansio testeille.

Yksi projekti vastaa yhtä työaluetta. Go:ssa näin ei ole. Go:ssa on ainoastaan yksi ainoa työalue, jonka alla kaikki koodi on.

Go ymmärtää projektit omiksi kokonaisuuksikseen kansiorakenteiden ja määreen `package <name>` avulla.

Käyttäjällä on oma Go-alueensa, joka on määritetty `GOPATH` ympäristömuuttujan avulla. Minun GOPATH on asetettu seuraavanlaiseksi:

```sh
❯ echo $GOPATH
/home/greatman/Code/go
```

Tässä kansiossa listaus antaa seuraavan:

```sh
❯ ls
bin  pkg  src
```

Jos asentaa Go:lla, binäärit menevät bin kansioon. Go voi käyttää githubbia myös lähteenä, eli github toimii Go:n yhtenä pakettivarastona. (Go-kielen asennuksen yhteydessä tulee go-kielisten ohjelmien asennukseen ja hallintaa liittyvää softaa)

Go ei ainakaan oletuksena jätä lähteitä lataamatta. Oikeastaan tietääkseni (lähes?) kaikki Go:n asennukset tehdään kääntämällä lähdekoodi ja asentamalla siitä tuleva binääri edellä mainittuun bin kansioon.

Mielenkiintoisinta on siis src kansio. Sen sisältö syvyyteen 2 ja vain kansiot näyttää seuraavalta:

```sh
❯ tree -L 2 -d src
src
├── github.com
│   ├── alecthomas
│   ├── bep
│   ├── BurntSushi
│   ├── cpuguy83
│   ├── davidrjenni
│   ├── dchest
│   ├── dominikh
│   ├── eknkc
│   ├── fatih
│   ├── fsnotify
│   ├── golang
│   ├── gorilla
│   ├── Gredu
│   ├── hashicorp
│   ├── josharian
│   ├── jstemmer
│   ├── kardianos
│   ├── kisielk
│   ├── klauspost
│   ├── kyokomi
│   ├── magiconair
│   ├── miekg
│   ├── mitchellh
│   ├── nicksnyder
│   ├── nsf
│   ├── pelletier
│   ├── PuerkitoBio
│   ├── rogpeppe
│   ├── russross
│   ├── shurcooL
│   ├── spf13
│   ├── yosssi
│   └── zmb3
├── golang.org
│   └── x
├── gopkg.in
│   ├── alecthomas
│   └── yaml.v2
└── honnef.co
    └── go

```

Tämä projekti sisältää kansiossa github.com/Gredu/TiraLabraRegex . Asennuksesta tulevan binäärin nimi on TiraLabraRegex.

Lähteet:
  - [go-tiedostorakenne](https://golang.org/doc/code.html)
  - [go-projektin pystyttäminen](https://dave.cheney.net/2014/12/01/five-suggestions-for-setting-up-a-go-project)



