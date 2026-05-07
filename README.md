# Bezpečné Heslo — Generátor Silných Hesiel

Jednoduchý generátor hesiel, ktorý funguje priamo v prehliadači.
Nie je potrebná inštalácia ani registrácia — stačí otvoriť súbor `bezpecne-heslo.html`.

---

## Funkcie

* Generuje bezpečné a náhodné heslá
* Funguje offline priamo vo vašom zariadení
* Nepoužíva server ani neodosiela údaje na internet
* Možnosť nastaviť:
  * dĺžku hesla
  * počet číslic
  * počet špeciálnych znakov

* Možnosť vypnúť podobné znaky (`O`, `0`, `I`, `1`, `l`)
* Zobrazuje silu hesla
* Umožňuje rýchle kopírovanie do schránky
* Pamätá si posledné nastavenia

---

## Ako používať

1. Stiahnite a otvorte súbor `bezpecne-heslo.html`
2. Nastavte požadované parametre
3. Kliknite na **Generovať**
4. Hotové heslo môžete skopírovať tlačidlom **Kopírovať**

---

## Ako sa hodnotí sila hesla

Aplikácia odhaduje bezpečnosť hesla podľa:

* dĺžky hesla
* použitých znakov
* náhodnosti generovania

### Úrovne sily hesla

| Úroveň | Hodnotenie  |
| ------ | ----------- |
| 1      | Veľmi slabé |
| 2      | Slabé       |
| 3      | Primerané   |
| 4      | Silné       |
| 5      | Veľmi silné |

---

## Bezpečnostné informácie

* Heslá sa generujú iba vo vašom prehliadači
* Žiadne heslá sa neukladajú ani neposielajú na internet
* Používa sa moderný bezpečný generátor náhodných hodnôt (`crypto.getRandomValues()`)

---

## Podporované prehliadače

Funguje vo všetkých moderných prehliadačoch:

* Chrome
* Firefox
* Edge
* Safari

---

## Štruktúra projektu

```text
bezpecne-heslo/
└── index.html
```

Celá aplikácia je v jednom súbore.

---

## Licencia

MIT — projekt môžete voľne používať a upravovať.

