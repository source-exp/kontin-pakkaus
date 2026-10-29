# Määrittelydokumentti

## Hallinnolliset tiedot
* **Opinto-ohjelma:** Tietojenkäsittelytie­teen kandiohjelma
* **Dokumentaation kieli:** Suomi
* **Käytettävä ohjelmointikieli:** Python
* **Muut hallittavat ohjelmointikielet (vertaisarviointia varten):** Lua, JavaScript / TypeScript

## Ratkaistava ongelma
Rahtifirma NopsaToimitus haluaa optimoida konttikuljetuksissa käytettävän tilan. Tavoitteena on pakata paketit konttiin mahdollisimman tehokkaasti, kun tiedetään pakettien mitat ja kontin mitat.

Pakettien täytyy mahtua kontin sisälle sillä tavalla, että ne eivät leikkaa toisiaan. Mahdollisesti paketteja voidaan kääntää (`90°`:n kulmissa). Tämä on tunnetusti NP-kova ongelma. Lopputulos visualisoidaan, jotta onnistumista voidaan arvioida silmämääräisesti.

## Harjoitustyön ydin
Harjoitustyön ydin on kolmiulotteisen pakkausalgoritmin tehokas toteuttaminen. Suurin osa kehitysajasta kuluu juuri algorimin toimivuuteen, pakettien optimaalisen järjestyksen valintaan ja kontin täyttöasteen maksimointiin. Tuloksen arviointiin pitää lisäksi kehittää kolmiulotteinen visualisointi ja syötteiden lukeminen.

## Aihe ja toteutus

### Algoritmit
1. **First Fit Decreasing (FFD) tai Best Fit Decreasing (BFD):**:
   * Paketit järjestetään tilavuuden tai pisimmän sivun mukaan järjestykseen.
   * Sen jälkeen paketit sijoitettaan kontteihin yksi kerrallaan.
2. **Extreme Points (EP):**
   * Kun paketti asetetaan konttiin, se luo ääripisteitä paketin kulmien viereen: `(x + leveys, y, z)`, `(x, y + korkeus, z)` ja `(x, y, z + syvyys)`.
   * Sen jälkeen pakettia yritetään sijoittaa näihin pisteisiin sillä tavalla, että ne jättävät mahdollisimman vähän hukkatilaa.

### Tietorakenteet
* **Paketti:** Paketin mitat `(w, h, d)` ja sijoituskoordinaatit `(x, y, z)` kontissa.
* **Kontti:** Kontin mitat `(W, H, D)`, lista sinne sijoitetuista paketeista ja lista vapaista sijoituspisteistä.
* **Dynaamiset taulukot/listat ja prioriteettijono:** Lista paketeista, joista jokaisella on tunniste, sekä kyseisen pakettityypin lukumäärä.

### Syötteet ja tulokset
* **Syötteet:** Kontin mitat `(W, H, D)` ja pakettien tiedot, muodossa JSON, CSV tai komentoriviparametreina.
* **Tulokset:** Tilastotiedot komentoriville ja 3D-visualisointi, jossa paketit ovat eri värisiä ja käyttäjä voi pyörittää mallia.

## Aika- ja tilavaativuus

### Aikavaativuus
1. **Pakettien järjestäminen (Merge Sort):** `O(n log n)`.
2. **Pakettien sijoittaminen (FFD/BFG + EP):** Koska jokainen uusi sijoitettu paketti luo 3 uutta pistettä, kontissa on korkeintaan `O(n)` pistettä. Tällöin yhden paketin sijoittaminen voi viedä enintään `O(n^2)` ja kaikkien `n` paketin sijoittaminen vie kokonaisuudessaan aikaa **`O(n^3)`**.

### Tilavaativuus
* **Tavoite:** **`O(n)`**
* Ohjelman tarvitsee pitää muistissa `n` pakettia, enintään `n` konttia sekä korkeintaan `3n` pistettä. Eli nämä kasvavat lineaarisesti syötteen koon `n` suhteen.

## Lähteet
1. Bin packing problem(Wikipedia): [Bin packing problem](https://en.wikipedia.org/wiki/Bin_packing_problem)
2. Extreme Point-Based Heuristics for Three-Dimensional Bin Packing (2007): [Extreme Point-Based Heuristics for Three-Dimensional Bin Packing (2007)](https://www.cirrelt.ca/documentstravail/cirrelt-2007-41.pdf)
3. The Three-Dimensional Bin Packing Problem (1997): [The Three-Dimensional Bin Packing Problem (1997)](https://www.researchgate.net/publication/2353632_The_Three-Dimensional_Bin_Packing_Problem)
