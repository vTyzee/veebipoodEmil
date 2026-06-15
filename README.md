# Veebipood

Veebipood on lihtne Node.js ja Express.js põhine veebirakendus. Rakenduses saab vaadata tooteid, otsida tooteid, registreeruda, sisse logida ja luua tellimusi.

## Kasutatud tehnoloogiad

* Node.js
* Express.js
* JavaScript
* HTML
* CSS
* Docker
* GitHub Actions

## Käivitamine

Projekti käivitamiseks tuleb paigaldada sõltuvused:

```bash
npm install
```

Serveri käivitamiseks:

```bash
npm start
```

Rakendus avaneb aadressil:

```text
http://localhost:3000
```

Testide käivitamiseks peab server töötama. Testid saab käivitada käsuga:

```bash
node src/test.js
```

## Parandatud vead

Projektis parandati kaks viga.

Esimene viga oli failis `src/routes/products.js`. Toodete otsing ei töötanud õigesti, sest kasutati valet andmemassiivi `data.items`. See parandati nii, et otsing kasutab nüüd õiget massiivi `data.products`.

Teine viga oli failis `src/routes/orders.js`. Uue tellimuse staatus oli alguses vale. Varem oli staatus `"pending"`, aga ülesande järgi peab tellimuse staatus olema `"vastu võetud"`. See viga parandati.

Pärast parandusi läbivad kõik testid:

```text
Tulemused: 11 läbis, 0 ebaõnnestus
```

## API endpointid

### Tooted

* `GET /api/products` - tagastab kõik tooted
* `GET /api/products/:id` - tagastab ühe toote ID järgi
* `GET /api/products/search?name=...` - otsib tooteid nime järgi
* `GET /api/products/categories` - tagastab tootekategooriad
* `GET /api/products/category/:cat` - tagastab kindla kategooria tooted

### Kasutajad

* `POST /api/users/signup` - loob uue kasutaja
* `POST /api/users/login` - logib kasutaja sisse
* `POST /api/users/logout` - logib kasutaja välja
* `GET /api/users/me` - tagastab sisselogitud kasutaja andmed

### Tellimused

* `POST /api/orders` - loob uue tellimuse
* `GET /api/orders` - tagastab kõik tellimused
* `GET /api/orders/me` - tagastab kasutaja tellimused
* `GET /api/orders/:id` - tagastab ühe tellimuse
* `PATCH /api/orders/:id/status` - muudab tellimuse staatust

### Statistika

* `GET /api/stats` - tagastab rakenduse statistika
* `GET /health` - kontrollib serveri töötamist

## Arhitektuuri analüüs

Projekt kasutab lihtsat monoliitset klient-server arhitektuuri. Frontend asub `public` kaustas ning koosneb HTML ja CSS failidest. Backend asub `src` kaustas ning kasutab Node.js ja Express.js raamistikku.

Serveri põhifail on `src/server.js`. API loogika on jagatud eraldi failidesse `src/routes` kaustas. Näiteks toodetega seotud loogika asub failis `products.js`, kasutajatega seotud loogika failis `users.js` ja tellimustega seotud loogika failis `orders.js`.

Andmeid hoitakse failis `src/data.js`. Projekt ei kasuta päris andmebaasi, vaid hoiab andmeid rakenduse sees. Selline lahendus sobib õppimiseks ja väikese projekti jaoks, sest seda on lihtne käivitada ja testida.

Selle põhjal saab järeldada, et tegemist ei ole mikroteenuste arhitektuuriga. Kõik funktsioonid töötavad ühes rakenduses ja ühes serveris. Samuti ei ole siin ranget MVC struktuuri, sest mudelid, vaated ja kontrollerid ei ole täielikult eraldi kihtidena jagatud.

Arendajad valisid tõenäoliselt sellise arhitektuuri, sest projekt on väike ja mõeldud õppimiseks. Monoliitset Express.js rakendust on lihtne mõista, parandada ja edasi arendada. Kui rakendus peaks tulevikus teenindama väga palju kasutajaid, oleks mõistlik lisada päris andmebaas, eraldi frontend ja parem autentimissüsteem.

## GitHub Actions

Projektis on lisatud GitHub Actions workflow fail `.github/workflows/ci.yml`. See käivitab automaattestid iga pushi ja pull requesti korral.

Pipeline teeb järgmised sammud:

1. Laeb projekti koodi alla.
2. Paigaldab Node.js keskkonna.
3. Paigaldab sõltuvused käsuga `npm install`.
4. Käivitab serveri.
5. Käivitab testid käsuga `node src/test.js`.

See aitab kontrollida, et katkine kood ei jõuaks main harusse.


## Monoliit -> Micro 
Kui minna monoliitselt arhitektuurilt üle mikroteenustele, siis muutuks süsteem paremini skaleeritavaks. Näiteks kasutajate, toodete ja tellimuste loogika saaks jagada eraldi teenusteks ning iga teenust oleks võimalik eraldi arendada, testida ja vajadusel suurema koormuse jaoks eraldi käivitada. Samas muutuks süsteem keerulisemaks, sest oleks vaja lahendada teenuste omavaheline suhtlus, andmebaaside haldus, autentimine, logimine ja deployment. Selle projekti jaoks ei ole mikroteenused praegu vajalikud, sest rakendus on väike ja monoliit on lihtsam ning mõistlikum valik.
Lisainfo: [Monoliidilt mikroteenustele �leminek](MIKROTEENUSED.md)

