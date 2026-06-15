# Monoliidilt mikroteenustele üleminek

Praegune veebipoe rakendus kasutab monoliitset klient-server arhitektuuri. See tähendab, et kogu backend töötab ühes Node.js ja Express.js rakenduses ning kasutajate, toodete ja tellimuste loogika asub samas projektis. Selline lahendus sobib hästi väikese laboritöö või õppimiseks mõeldud projekti jaoks, sest seda on lihtne käivitada, testida ja parandada.

Kui rakendus kasvaks suuremaks ja peaks teenindama näiteks väga palju kasutajaid, võiks kaaluda üleminekut mikroteenuste arhitektuurile. Sellisel juhul jagataks süsteem väiksemateks eraldi teenusteks. Näiteks võiks olla eraldi kasutajate teenus, toodete teenus, tellimuste teenus ja statistika teenus. Iga teenus vastutaks ainult ühe kindla osa eest.

Mikroteenuste kasutamise peamine eelis on parem skaleeritavus. Kui näiteks toodete otsingule tuleb palju päringuid, saab just toodete teenust eraldi suurendada, ilma et peaks kogu rakendust korraga muutma. Samuti saavad arendajad töötada erinevate teenuste kallal iseseisvamalt ning ühe teenuse viga ei pruugi kogu süsteemi täielikult maha võtta.

Samas muudaks mikroteenustele üleminek projekti palju keerulisemaks. Teenused peaksid omavahel suhtlema API-de kaudu, vaja oleks lahendada autentimine, logimine, andmebaaside haldus, deployment ja vigade jälgimine. Lisaks oleks vaja kasutada rohkem tööriistu, näiteks Dockerit, CI/CD lahendusi, API gateway'd ja võib-olla ka sõnumijärjekordi.

Selle veebipoe projekti jaoks ei ole mikroteenused praegu vajalikud. Rakendus on väike, andmed asuvad ühes failis ja kogu funktsionaalsus mahub ühte Express.js serverisse. Seetõttu on monoliitne arhitektuur siin lihtsam ja mõistlikum valik. Mikroteenustele oleks mõtet üle minna alles siis, kui projekt kasvab suuremaks, kasutajaid on palju ja erinevaid süsteemi osi on vaja eraldi skaleerida.
