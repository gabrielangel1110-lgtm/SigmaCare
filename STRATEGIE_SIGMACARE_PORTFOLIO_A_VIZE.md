# SigmaCare – portfolio, strategická vize a produktové větve

**Stav:** pracovní strategie, 27. 10. 2026. **Priorita:** nejprve definice cílů a produktů, teprve potom výběr technologií. Tento dokument vychází z uživatelského popisu a dodaného referenčního diagramu SigmaAI. Není ověřením komerční nabídky, provozního stavu ani hotových funkcí SigmaCare.

## 1. Co je SigmaCare
SigmaCare je podle dosavadního popisu iniciativa/společnost zaměřená na datově podložené řízení zdravotnických provozů: analytiku, predikce, ekonomiku případů, plánování kapacit a vzdělávání v řízení změn. Její produkty mají sloužit nejen k reportování, ale k lepšímu rozhodování a změnám pracovních procesů.

## 2. Produktové portfolio – pracovní mapa

| Větev | Zaměření dle popisu | Co je zatím doloženo | Potenciální rozvoj |
|---|---|---|---|
| **SigmaOR** | Operační sály, vytíženost, plánování, predikce, simulace scénářů; související lůžkové kapacity | Uživatel popsal existující zaměření a predikční ambice; rozsah hotových simulací není ověřen | Digitální provozní model operačních sálů a lůžek, kapacitní scénáře |
| **SigmaHEART** | Kardiologie, výkony, materiál, ekonomické a provozní sledování | Uživatel popsal jako rozvinutou specializovanou oblast; přesné funkce nejsou ověřeny | Digitální řízení kardiologického pracoviště |
| **SigmaCALC** | Ocenění/nákladovost hospitalizačního případu, alokace nákladů nemocnice, trasování případu | Popsané zaměření; metodika a aktuální implementace neověřeny | Ekonomický model kliniky, cost-per-case, scénáře efektivity |
| **Sigma Academy** | Workshopy a vzdělávání v Lean/Green managementu, optimalizaci a změně chování zaměstnanců | Popsané vzdělávací aktivity; nabídka a výsledky neověřeny | Podpora implementace změn na základě analytických zjištění |
| **SigmaAI** | Společná agentní a analytická platforma nad projekty | Referenční diagram dodaný uživatelem, vývojový záměr | Automatické kontroly, anomálie, navazující analýzy, prioritizace, asistence |

**Důležitá terminologie:** „SigmaOR“ a „SigmaCOR“ mohou být různé názvy či vrstvy (produkt/reporting). V diagramu se objevuje SigmaAplikace; vztah názvů musí SigmaCare potvrdit. Stejně ověřit oficiální zápis SigmaHEART a SigmaCALC.

## 3. Vize (pracovní návrh)
**Od reportingu k aktivnímu řízení kliniky:** propojit produkci, kapacity, náklady, materiál, odborné metodiky a lidské rozhodování do jednoho průběžně vyhodnocovaného modelu. Nejprve **digitálně řízená klinika**, později potenciálně **digitálně řízená nemocnice**.

Nejde automaticky o plnohodnotné digitální dvojče; jeho rozsah (simulace, zpětná vazba, validace) se musí teprve definovat.

## 4. Strategické cíle a výsledky
1. **Transparentnost:** klinika zná aktuální výkonnost, náklady a využití zdrojů. Výsledek: jednotné, ověřené KPI a metodiky.
2. **Předvídavost:** umí odhadovat vývoj a testovat scénáře. Výsledek: validované predikce a porovnání scénářů.
3. **Proaktivní controlling:** systém sám kontroluje desítky klinik a prioritizuje důležité odchylky. Výsledek: dohledatelné nálezy, nikoli záplava upozornění.
4. **Ekonomika případu:** porozumění skutečné nákladovosti a jejím příčinám. Výsledek: transparentní kalkulace a rozpad nákladů.
5. **Realizace změn:** analytické poznatky vedou k ověřitelným opatřením. Výsledek: rozhodnutí, vlastník úkolu, kontrola dopadu; Academy podporuje adopci.
6. **Škálování:** společná technologie pro více klientů, oddělená data a oprávnění. Výsledek: rychlé zavedení další kliniky bez kopírování celé aplikace.

## 5. Strategické větve rozvoje
- **A. Provoz a kapacity (SigmaOR):** sály, plán, skutečnost, délky výkonů, zrušení, návaznost lůžek, scénáře.
- **B. Specializovaná klinická doména (SigmaHEART):** kardiologické procesy, výkony, materiály a ekonomika.
- **C. Ekonomika a nákladovost (SigmaCALC):** hospitalizační případ, alokace, nákladové faktory, DRG kontext.
- **D. Lidé a změna (Sigma Academy):** vzdělávání, Lean/Green, zavádění doporučení, zpětná vazba.
- **E. Průřezová inteligence (SigmaAI):** monitoring, analytické hypotézy, vysvětlení, doporučení, interaktivní práce, bezpečné oddělení projektů.

## 6. Co už máme / co zatím nevíme
| Téma | Známe z popisu/diagramu | Je třeba ověřit |
|---|---|---|
| Datové prostředí | Azure Data Lake, datový sklad/CSV, číselníky, primární a zpracovaná data, reporting | Úplnost, konkrétní formáty, odpovědnosti a aktuální stav |
| Transformace/predikce | IBM SPSS Modeler, Python výpočty, predikce; pilot Fabric zmíněn | Konkrétní modely, kvalita, dostupnost, validace |
| Uživatelské prostředí | SigmaAplikace/SharePoint/Power BI/AI chat v referenčním návrhu | Co je již provozováno a co je návrh |
| AI platforma | Referenční návrh SigmaAI s agentní vrstvou a AI Gateway | Realizované části, rozpočet, priority a produktové požadavky |
| Produkty | OR, HEART, CALC, Academy podle popisu | Vlastníci, uživatelé, zralost, obchodní model a KPI úspěchu |

## 7. Postup shora dolů – bez předčasného výběru technologií
**Etapa 0: Strategická inventura.** Pro každou větev potvrdit produkt, uživatele, problém, dnešní stav a dlouhodobý cíl.
**Etapa 1: Produktová mapa.** Popsat schopnosti a konkrétní uživatelské scénáře; oddělit hotové, rozpracované, plánované.
**Etapa 2: Prioritizace.** Hodnota pro klienta, proveditelnost, dostupnost dat, bezpečnost, opakovatelnost mezi klinikami.
**Etapa 3: Pilot hodnoty.** Vybrat jeden konkrétní problém, stanovit měřitelné výsledky a akceptační kritéria.
**Etapa 4: Provozní model.** Odpovědnosti, metodiky, kvalita, podpora, vzdělávání, verzování, bezpečnost a finance.
**Etapa 5: Technická architektura.** Až nyní volit Fabric/Foundry/LLM/Python/MCP a hosting podle požadavků.

## 8. Otázky pro další strategické setkání
1. Jak SigmaCare samo definuje své čtyři produktové větve a vztah SigmaAI k nim?
2. Co už je reálně nasazené, co pilotní a co jen vize? Pro každou větev konkrétní příklad.
3. Kdo jsou cíloví zákazníci a uživatelé jednotlivých produktů?
4. Jaké tři problémy nemocnic mají největší obchodní a klinicko-provozní význam?
5. Jaký je cílový model „digitální kliniky“? Co musí řídit, předvídat a simulovat?
6. Které funkce mají být společné napříč klinikami a které doménově specifické?
7. Jak budou měřeny přínosy, správnost zjištění a dopad změn?
8. Kdo vlastní metodiky, datové modely, kvalitu a zákaznickou podporu?
9. Co je nejbližší produktový milník a co vědomě odložíme?
10. Jak má Sigma Academy pomoci proměnit analytické závěry ve skutečnou změnu?

## 9. Referenční architektura
Viz [SigmaAI – referenční architektura](SigmaAI/REFERENCNI_ARCHITEKTURA.md). Původní uživatelem dodaný obrázek je zdrojovým podkladem; binární kopii obrázku je ještě nutné vložit do repozitáře.
