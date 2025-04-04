- Cílem je zajistit, aby systém i přes chyby v jednotlivých uzlech nebo komponentách fungoval spolehlivě, udržoval konzistentní stav a poskytoval očekávané služby.

- Selhání uzlů nebo komunikačního kanálu vede k chybám.
- Obecně by měly DS tolerovat určité množství chyb.

>[!Example] Základní vlastnosti DS:
>- **Dostupnost** - dostupnost systému v čase
>- **Spolehlivost** - doba běhu bez chyb
>- **Bezpečnost** - nedojde ke katastrofickému selhání při chybě
>- **Udržovatelnost** - jak snadno lze odstranit chyby

- Vysoká dostupnost vs. vysoká spolehlivost.
- Různé metriky
	- MTTF - Mean Time To Failure
	- MTTR - Mean Time To Repair
	- MTBF - Mean Time Between Failures

## Klasifikace chyb
### Podle trvání
- Přechodná (transient) - objeví se jednou a zmizí.
	- Třeba výpadek signálu.
- Přerušovaná (intermittent) - chyba se objevuje a mizí.
	- Chvíli funguje vpohodě, pak chyba, pak vpohodě, ...
- Trvalá (permanent) - chyba zůstává do vyřešení.
	- Objeví a už nezmizí (např. odejde HDD).

### Podle projevu

| chyba           | popis                                           |
| --------------- | ----------------------------------------------- |
| stop chyba      | server se vypne, až do chyby funguje správně    |
| chyba vynechání | selhání poslání či přijetí zprávy               |
| chyba časování  | odpověď není doručena v daném časovém intervalu |
| chyba odpovědi  | odpověď je nesprávná                            |
| náhodná chyba   | (Byzantská) náhodná odpověď v libovolném čase   |
### Selhání uzlu
- V **asynchronních systémech** je **obtížné přímo určit, že nastala chyba**.
	- Komunikace probíhá **bez** nějakého **pevného časového rámce** a tudíž detekce chyby může být komplikovaná.
- V **synchronních systémech** existuje **časový rámec pro vykonání operací a doručení zpráv**.
	- *Selhání uzlu může být detekováno, pokud nedojde k očekávané akci v daném časovém rámci.*
- **Částečně-synchronní systémy** jsou jako **synchronní systémy bez omezení času.**
	- Pro synchronizace se využívají **časovače**.
	- Částečně synchronní systémy jsou často *využívány v odvětvích, kde je potřeba nějaká synchronizace*, ale **úplně synchronní systémy by byly příliš restriktivní nebo nemožné**.

### Modely detekce chyb
- **Fail-stop**:
	- Okamžité ukončení a spolehlivá detekce chyby.
- **Fail-noisy**:
	- Eventuálně spolehlivě detekovatelné.
- **Fail-silent**:
	- Nelze rozlišit pád a vynechání.
	- Např. Nevíme, jestli nefunguje uzel nebo kanál.
- **Fail-safe**:
	- O chybě nevíme nic, ale chyby jsou neškodné.
- **Fail-arbitrary**:
	- O chybě nevíme nic. 
	- Teoreticky může způsobit katastrofu.

## Redundance
- **Základní nástroj** pro konstrukci distribuovaných systémů s tolerancí chyb.
Druhy redundance:

| Druh                  | Popis                                                                                                                                                                                                                       |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Informační redundance | Je záměrně zavedena za *účelem zvýšení spolehlivosti, bezpečnosti nebo odolnosti vůči chybám* v **přenosu nebo zpracování inforací** (například paritní bity, kontrolní součty, duplikace dat, ...)                         |
| Časová redundance     | Je využíván v různých oblastech, kde **opakování časových vzorků nebo operací může přinést nějaký užitek**, zejména v kontextu spolehlivosti, bezpečnosti nebo odolnosti vůči chybám (například opětovné odvysílání zprávy) |
| Fyzická redundance    | Týká se **opakování nebo zdvojení fyzických prvků nebo komponent v systému** s cílem *zvýšit spolehlivost, dostupnost nebo odolnost vůbec chybám* (například záložní uzly, servery, napájení, propojení, RAID, ...)         |
- Systém je **$k$-tolerantní** pokud **přežije výpadek $k$ uzlů**.

>[!Example] Použitím redundance:
>- Zavádíme abstrakci (komunikujeme se skupinou na místo jednoho uzlu)
>- Skupiny jsou dynamické (mohou vznikat, zanikat, uzly odchází, přichází nebo mohou být součástí více skupin)
>- Organizace uvnitř skupiny, může být rozdílná podle potřeb.

## Tolerance Byzantských chyb: Idea
- **Byzantská chyba v kontextu DS** se vztahuje k situaci, kdy *některé uzly nebo části systému mohou selhat* a **chovat se nespolehlivě**.
- Může zahrnout i **záměrné škodlivé chování**.
- Termín vychází z myšlenky, že **byzantský generál**, který vede armádu, se může rozhodnout jednat zrádně a poslat falešné informace či dokonce úplně selhat.

- Tolerování $m$ Byzantských chyb vyžaduje $3m+1$ uzlů.
- Shoda je na **rozhodnutí většiny**.
- Vyžaduje **exponenciální počet zpráv** (velice nákladné).

>[!Example] Postup:
>- Máme **server**, který předá zprávu uzlům
>- Ty si pak **mění zprávy mezi sebou** a **odpovědi** od kolegů **si značí do tabulky**
>- Podle tabulky vyhodnotí výsledek (podle většiny) a znovu si přepošle s ostatními
>- Následně **dochází ke shodě**
>![[MacBook-2025-01-05-002372.png]]

<div style="text-align: center; margin-top: 20px;">
    <!-- Horní tlačítka -->
    <div style="display: flex; justify-content: center; gap: 10px; margin-bottom: 10px;">
        <a href="obsidian://open?vault=SZZ-Otazky2024&file=Obor%20AINF-VS%2FPovinn%C4%9B%20voliteln%C3%A9%20p%C5%99edm%C4%9Bty%2FShoda%20v%20DS" style="text-decoration: none;">
            <button style="padding: 10px 20px; background-color: #007BFF; color: white; border: none; border-radius: 5px; cursor: pointer;">
                Předchozí otázka
            </button>
        </a>
        <a href="obsidian://open?vault=SZZ-Otazky2024&file=Obor%20AINF-VS%2FPovinn%C4%9B%20voliteln%C3%A9%20p%C5%99edm%C4%9Bty%2FGlob%C3%A1ln%C3%AD%20stav%20v%20DS" style="text-decoration: none;">
            <button style="padding: 10px 20px; background-color: #007BFF; color: white; border: none; border-radius: 5px; cursor: pointer;">
                Následující otázka
            </button>
        </a>
    </div>
    <!-- Spodní tlačítko -->
    <a href="obsidian://open?vault=SZZ-Otazky2024&file=Obor%20AINF-VS%2F2.%20Povinn%C4%9B%20voliteln%C3%A9%20p%C5%99edm%C4%9Bty" style="text-decoration: none;">
        <button style="padding: 15px 30px; background-color: #ADD8E6; color: black; border: none; border-radius: 5px; cursor: pointer; width: 43%;">
            Všechny otázky
        </button>
    </a>
</div>