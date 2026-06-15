# Mikroteenused

See kaust on näide sellest, kuidas praegust monoliitset veebipoe rakendust saaks tulevikus jagada mikroteenusteks.

Main harus jääb alles töötav monoliitne versioon, mis sobib laboritöö esitamiseks. See `mikroteenused` haru on eraldi koopia, kus näidatakse võimalikku uut struktuuri ilma põhiprojekti rikkumata.

## Praegune struktuur

Praeguses versioonis töötab kogu backend ühe Node.js ja Express.js serverina. Frontend asub `public` kaustas, backend asub `src` kaustas ning API loogika on jagatud `src/routes` failidesse.

See tähendab, et kasutajate, toodete, tellimuste ja statistika loogika on ühes rakenduses. Sellist lahendust nimetatakse monoliitseks klient-server arhitektuuriks.

## Mikroteenuste struktuur

Mikroteenuste arhitektuuris võiks rakenduse jagada väiksemateks eraldi teenusteks:

```text
Mikroteenused/
  gateway-service/
  user-service/
  product-service/
  order-service/
  stats-service/
  shared/
```

## gateway-service

`gateway-service` oleks API gateway. See võtaks vastu kliendi päringud ja suunaks need õigesse teenusesse.

Näiteks:

* `/api/users` läheks `user-service` teenusesse
* `/api/products` läheks `product-service` teenusesse
* `/api/orders` läheks `order-service` teenusesse
* `/api/stats` läheks `stats-service` teenusesse

Gateway aitab peita kliendi eest seda, et backend koosneb mitmest eraldi teenusest.

## user-service

`user-service` vastutaks kasutajatega seotud loogika eest.

Sinna kuuluksid näiteks:

* kasutaja registreerimine
* sisselogimine
* väljalogimine
* aktiivse kasutaja andmete küsimine
* sessioonide või tokenite kontroll

Selle teenuse aluseks on praegune `src/routes/users.js`.

## product-service

`product-service` vastutaks toodetega seotud loogika eest.

Sinna kuuluksid näiteks:

* kõikide toodete kuvamine
* ühe toote otsimine ID järgi
* toodete otsing nime järgi
* kategooriate kuvamine
* toodete filtreerimine kategooria järgi

Selle teenuse aluseks on praegune `src/routes/products.js`.

## order-service

`order-service` vastutaks tellimustega seotud loogika eest.

Sinna kuuluksid näiteks:

* uue tellimuse loomine
* kõikide tellimuste kuvamine
* kasutaja enda tellimuste kuvamine
* ühe tellimuse kuvamine
* tellimuse staatuse muutmine

Selle teenuse aluseks on praegune `src/routes/orders.js`.

## stats-service

`stats-service` vastutaks statistika eest.

Sinna võiks kuuluda näiteks:

* toodete arv
* kasutajate arv
* tellimuste arv
* aktiivsete tellimuste arv

Praeguses monoliidis on statistika ühe serveri sees, aga mikroteenuste korral võiks see olla eraldi teenus.

## shared

`shared` kaustas on ühised failid, mida erinevad teenused võiksid kasutada. Näiteks praeguses lihtsas projektis on andmed failis `src/data.js`, seega kopeeriti see kausta `Mikroteenused/shared/data.js`.

Päris mikroteenuste arhitektuuris ei oleks tavaliselt üks ühine `data.js` fail parim lahendus. Igal teenusel võiks olla oma andmebaas või vähemalt oma andmemudel. Selle laboritöö jaoks on see aga lihtne viis näidata, kuidas olemasolevat monoliiti saaks loogiliselt jagada.

## Mis muutuks mikroteenustele üleminekul?

Kui minna monoliitselt arhitektuurilt üle mikroteenustele, muutuks süsteem paremini skaleeritavaks. Näiteks kui toodete otsingule tuleb palju päringuid, saab suurendada ainult `product-service` teenust, mitte kogu rakendust.

Samuti oleks võimalik teenuseid eraldi arendada, testida ja kasutusele võtta. See tähendab, et ühe teenuse muutmine ei nõua alati kogu süsteemi muutmist.

Mikroteenuste korral saaks iga teenust vajadusel eraldi deploy'da. Näiteks kui muudetakse ainult tellimuste loogikat, siis piisaks `order-service` uuendamisest. See vähendaks riski, et ühe väikese muudatuse pärast tuleb kogu backend uuesti välja panna.

Samas muutuks süsteem keerulisemaks. Oleks vaja lahendada teenuste omavaheline suhtlus, autentimine, logimine, vigade jälgimine, andmebaaside haldus ja deployment. Samuti oleks vaja näiteks API gateway'd ja tõenäoliselt Dockerit või mõnda muud konteinerlahendust.

Selle veebipoe laboritöö jaoks on monoliit parem valik, sest projekt on väike ja õppimiseks mõeldud. Mikroteenuste struktuur on siin lisatud näitena, kuidas rakendust võiks tulevikus suuremaks süsteemiks ümber kujundada.
