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