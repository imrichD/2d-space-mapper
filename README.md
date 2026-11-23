
# Automatický 2D mapovač priestoru

Semestrálny projekt z predmetu **Vnorené riadiace systémy (VRS)**, FEI STU Bratislava.

**Tím:** Dzvoňár, Ďurmek, Nebus, Vozárik  
**Platforma:** STM32 Nucleo-F303K8, firmvér v jazyku C (STM32CubeIDE)

---

## 1. Popis projektu

Cieľom projektu je vytvoriť **prenosné zariadenie na automatické 2D mapovanie vnútorných priestorov** pomocou senzora vzdialenosti umiestneného na otočnej platforme s krokovým motorom.

Zariadenie na zvolenom stanovisku vykoná **360° sken okolia**, pričom zaznamenáva namerané vzdialenosti a príslušné uhly. Z týchto údajov sa vytvorí 2D mapa okolia.

Na mapovanie väčších priestorov alebo viacerých prepojených miestností bude možné zariadenie **ručne premiestňovať medzi stanoviskami**. Jednotlivé skeny sa následne spoja do spoločnej mapy pomocou algoritmu **Scan Matching** (predbežne Correlative Scan Matching), s možnosťou manuálneho zarovnania.

### Hlavné funkcie

1. Automatické 360° skenovanie s nastaviteľným uhlovým krokom.
2. Meranie vzdialeností a spracovanie nameraných údajov.
3. Riadenie krokového motora a určovanie uhlovej polohy senzora.
4. Komunikácia medzi STM32 a PC.
5. Vizualizácia jednotlivých skenov.
6. Spájanie skenov z viacerých stanovísk do spoločnej 2D mapy.

---

## 2. Hardvérové vybavenie

| Komponent | Účel |
|---|---|
| STM32 Nucleo-F303K8 | Riadiaca jednotka |
| Senzor vzdialenosti | Meranie vzdialeností |
| Krokový motor a driver | Otáčanie senzora |
| Otočná platforma a podstavec | Mechanická konštrukcia |
| Napájanie | Napájanie zariadenia |

---

## 3. Rozdelenie úloh

### Dzvoňár: Zostavovanie a spájanie skenov

- Vytvorenie modulu na STM32, ktorý spája namerané vzdialenosti s príslušnými uhlami a zostavuje údaje jednotlivých skenov.
- Príprava údajov skenov na odoslanie a ďalšie spracovanie.
- Implementácia algoritmu Correlative Scan Matching na výpočet vzájomnej polohy a orientácie skenov.
- Overenie správnosti spájania skenov z rôznych stanovísk.

### Nebus: Senzor vzdialenosti a hardvér

- Implementácia ovládača senzora vzdialenosti na STM32.
- Čítanie, kontrola a filtrácia nameraných vzdialeností.
- Kalibrácia a overenie presnosti merania.
- Návrh a realizácia mechanickej konštrukcie zariadenia.
- Zabezpečenie napájania zariadenia.

### Ďurmek: Komunikácia a vizualizácia

- Implementácia komunikácie medzi STM32 a PC.
- Príjem príkazov a odosielanie nameraných údajov pomocou periférií STM32.
- Spracovanie prijatých údajov a vykresľovanie jednotlivých skenov na PC.
- Zobrazenie spoločnej mapy podľa výsledkov Scan Matchingu.
- Možnosť manuálneho zarovnania skenov.

### Vozárik: Pohon a riadenie zariadenia

- Implementácia ovládača krokového motora na STM32.
- Riadenie motora pomocou časovačov a prerušení.
- Softvérové určovanie uhlovej polohy a kalibrácia otáčania.
- Riadenie priebehu skenovania – postupné natáčanie senzora a spúšťanie meraní.
- Implementácia hlavného stavového automatu (spustenie, skenovanie, zastavenie, chyba).
- Integrácia modulov ostatných členov do spoločného firmvéru.

---

## 4. Overenie funkčnosti

- Overenie presnosti merania vzdialeností a uhlového polohovania.
- Vytvorenie 2D mapy z jedného stanoviska.
- Spojenie skenov z viacerých stanovísk do spoločnej mapy.
- Overenie mapovania viacerých prepojených miestností.
