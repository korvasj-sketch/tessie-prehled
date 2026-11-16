# Tessie — přehled nabíjení a kniha jízd

Webová aplikace (bez serveru): vytáhne z Tessie API nabíjení i jízdy za vybrané období,
seřadí je podle adresy a spočítá spotřebu. Export do Excelu.

## Spouštění

**Počítač — dvojklik na `index.html`** — otevře se v prohlížeči a funguje. Nic se nemusí instalovat.

**Mobil / cizí počítač — webová adresa:**
`https://korvasj-sketch.github.io/tessie-prehled/`
(token se tam zadává jednou do prohlížeče, pak už ne)

(Nebo přes server: `python -m http.server` → `http://127.0.0.1:8000/`.)

## Token (nemusíš ho psát pokaždé)

1. V Tessie: **Developer settings → Generate Access Token**.
2. Vlož ho do souboru **`config.js`** (leží vedle `index.html`):
   ```js
   window.TESSIE_CONFIG = { token: "TVOJ_TOKEN" };
   ```
3. Hotovo — aplikace si ho při každém spuštění přečte sama.

`config.js` se **do GitHubu nenahrává** (hlídá ho `.gitignore`), takže token zůstane
jen na tvém počítači. Změna tokenu = upravit tenhle soubor a uložit.

## GitHub — repozitář a webová verze

Repozitář: `https://github.com/korvasj-sketch/tessie-prehled`.
Obsahuje jen `index.html`, `README.md`, `.gitignore` — žádný token.

**Webová adresa (mobil):** `https://korvasj-sketch.github.io/tessie-prehled/`
- repo je veřejné (jen kód, token v něm NENÍ), Pages ho publikuje automaticky
- na mobilu se token zadá jednou a uloží se v prohlížeči telefonu
- `config.js` se na GitHub nenahrává — na počítači ho používá jen lokální verze

> Poznámka: GitHub Free umí Pages jen z veřejného repozitáře. Proto je rep veřejný —
> kdo by adresu znal, bez tvého tokenu neuvidí žádná data.

### Odeslání změn do GitHubu

```powershell
cd C:\Users\korva\Desktop\TessiePrehled
git add -A
git commit -m "popis změny"
git push
```

## Co umí

- výběr vozidla, období (od–do) + rychlé předvolby
- **Nabíjení**
  - filtr podle **místa nabíjení** (adresa + počet nabíjení) a typu (Supercharger / rychlé DC / AC)
  - souhrn podle místa: počet nabíjení, nabito kWh, průměr, spotřeba, náklady
  - **vlastní ceny** — do sloupce *Cena Kč/kWh* zapiš cenu pro dané místo (nebo *výchozí cenu*
    nad tabulkou); náklady se přepočítají v KPI, souhrnu, detailu i exportu a **uloží se samy**
  - detail každého nabíjení (časy, baterie %, odometr, náklady)
- **Kniha jízd**
  - filtr podle **místa (start nebo cíl)** a štítku jízdy
  - KPI: ujetá vzdálenost, spotřeba (kWh a na 100 km), počet jízd, čas za volantem
  - každá jízda zvlášť: odkud → kam, km, kWh, průměrná rychlost, doba, baterie
- **Vývoj po měsících** — sloupcový graf (kWh / km / Kč / počet nabíjení) za načtené období
- **Mapa jízd** (Leaflet + OpenStreetMap) — trasy start → cíl nebo místa nabíjení
  (Tessie ukládá jen začátek a konec jízdy, takže trasy jsou rovné linky)
- **Export do Excelu (.xlsx)** — všechny sekce tlačítkem; vždy jen samostatné řádky
  **bez součtů** (součty si dopočítáš v Excelu přes `SUM`), data ve formátu
  `DD.MM.YYYY HH:MM`, čísla jako čísla (jde sčítat)
- záložní export CSV (detail i souhrn) — otevře se v Excelu (česká diakritika)

## Bezpečnost

- token nikdy není v kódu ani v repozitáři — jen v `config.js` (lokálně) nebo
  v localStorage prohlížeče
- všechny požadavky chodí přímo z tvého prohlížeče na `api.tessie.com`,
  nikam jinam se nic neodesílá
