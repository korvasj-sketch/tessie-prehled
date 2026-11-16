# Tessie — přehled nabíjení

Webová aplikace (bez serveru): vytáhne z Tessie API nabíjení za vybrané období,
seřadí je podle místa a spočítá, kolik kWh jsi nabil (a za kolik).

## Spuštění lokálně

Stačí otevřít `index.html` v prohlížeči. (Nebo přes server: `python -m http.server`.)

## Nasazení na GitHub Pages (zdarma)

1. Na **github.com** → **New repository** (např. `tessie-prehled`) → zaškrtni **Public** → **Create repository**.
2. Klikni **uploading an existing file** → přetáhni `index.html` → **Commit changes**.
3. V repozitáři **Settings → Pages** → v sekci **Build and deployment**:
   - Source: **Deploy from a branch**
   - Branch: **main**, složka: **/ (root)** → **Save**.
4. Za minutu je stránka na adrese:
   `https://<tvuj-uzivatel>.github.io/tessie-prehled/`
   (adresa je i v Settings → Pages.)

## Token

- V Tessie: **Developer settings → Generate Access Token**.
- Token se vkládá do aplikace a ukládá **jen do tvého prohlížeče** (localStorage) —
  nikdy se nepíše do kódu ani do repozitáře (repo je veřejné!).
- Kdykoliv ho můžeš v Tessie vygenerovat znovu.

## Co umí

- výběr vozidla, období (od–do) + rychlé předvolby
- **Nabíjení**
  - filtr podle **místa nabíjení** (adresa + počet nabíjení) a typu (Supercharger / rychlé DC / AC)
  - souhrn podle místa: počet nabíjení, nabito kWh, průměr, spotřeba, náklady
  - detail každého nabíjení (časy, baterie %, odometr)
- **Kniha jízd**
  - filtr podle **místa (start nebo cíl)** a štítku jízdy
  - KPI: ujetá vzdálenost, spotřeba (kWh a na 100 km), počet jízd, čas za volantem
  - každá jízda zvlášť: odkud → kam, km, kWh, průměrná rychlost, doba, baterie
- **Export do Excelu (.xlsx)** — obě sekce tlačítkem; vždy jen samostatné řádky
  **bez součtů** (součty si dopočítáš v Excelu přes `SUM`), data ve formátu
  `DD.MM.YYYY HH:MM`, čísla jako čísla (jde sčítat)
- záložní export CSV (detail i souhrn) — otevře se v Excelu (česká diakritika)
