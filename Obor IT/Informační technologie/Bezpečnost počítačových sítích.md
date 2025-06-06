## Bezpečnost na úrovni fyzické vrstvy
- Zahrnuje:
	- Přerušení fyzické linky
	- Rušení a odposlech
- Zabránění odposlechu je obvykle zajištěno **omezeným přístupem k přenosovému médiu**.
- Na fyzické vrstvě jsou přenášena data ve formě bitů. **Nemá smysl uvažovat o modifikaci dat**.

## Bezpečnost na úrovni linkové vrstvy
- Kontrolní součet v linkových rámcích pomáhá odhalit pouze chyby přenosu (žádoucí rychlé spočítání a verifikace)
- Rizika:
	- Útočník může **snadno měnit obsah linkového rámce**. 
	- Útočník může **vytvářet umělé linkové rámce** a posílat je do sítě
	- Teoreticky je možné poslat BPDU (ze STP) rámce, které budou blokovat vytvoření topologie, nebo měnit topologii dle útočníkových požadavků.
	- Je **možné zahltit síť linkovými rámci**.
- Chránit se třeba pomocí *BPDU Guard* (Bridge protocol data unit)
- NIC jsou identifikována na základě MAC adresy.
	- Tu lze využít pro filtrování a omezení přístupu.
	- Problémy: 
		1) snadné podvržení
		2) útok na proces učení switche zasíláním podvržených linkových rámců
		3) přeplnění tabulky switche vymyšlenými MAC adresami

## Bezpečnost na úrovni síťové vrstvy
- Největší bezpečnostní problém je protokol IP.
	- Není šifrován, poskytuje pouze primitivní integrity dat.
- **IP pakety je možné snadno odposlouchávat**.
	- Není možné zabránit, jelikož data v hlavičce IP paketu jsou nezbytná pro směrování paketů.
	- Odposlechnutý paket je možné snadno modifikovat. Je tedy možné podvrhnout IP adresy odesílatele i příjemce, nebo zcela změnit data.
- Bezpečnost později přidána v podobě **protokolu IPSec** (IP Security).
	- IPSec poskytuje (transparentní) šifrování IP paketů a zabezpečuje jejich integritu a autentifikaci.
	- Umožňuje fungovat ve dvou režimech:
		1) Transportní režim (šifruje pouze data).
		2) Tunelovém režimu (šifruje celý paket).
- Další možností zabezpečení jsou **VPN** (*Virtual Private Network*).
	- Poskytují přístup do privátní sítě (bezpečné) sítě skrze veřejnou (nebezpečnou) síť.
	- Klient vytváří zabezpečený tunel s VPN serverem. Např. pomocí IPSec.

## Bezpečnost na úrovni transportní vrstvy
- Pro **pokročilejší filtraci** síťové komunikace.
- Typicky filtrace na základě portu, protokolu a stavu spojení.
- Díky portu můžeme realizovat plnohodnotný NAT.
- Navázání spojení = bezpečnostní problém, jelikož je možné jej snadno zneužít k realizaci DoS útoku.
	- Např. *SYN flooding útok* - útočník pošle mnoho TCP segmentů s příznakem SYN z různých IP adres. Z pohledu příjemce se jen někdo snaží navázat spojení. Příjemce odpoví segmentem s příznaky SYN a ACK a alokuje zdroje pro právě vznikající komunikaci.

## Bezpečnost na úrovni aplikační vrstvy
- Lze chápat jako **bezpečnost jednotlivých služeb**.
- Nejběžnějším bezpečnostním problémem jsou chyby v implementaci těchto služeb.
- Např. "Heartbleed" v OpenSSL.

##### Navigace
Předchozí:  [[Aplikační služby a tvorba síťových aplikací]]
Následující: [[Bezdrátové sítě - režimy, přenosové médium, problémy, bezpečnost]]
Celý okruh: [[2. Informační technologie]]