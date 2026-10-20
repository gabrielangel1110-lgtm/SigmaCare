# Sigma Care | Strategická diskuse 22. 10. 2026

**Stav:** Podklady k jednání, návrhy k rozhodnutí (nikoli schválené projekty).  
**Agenda:** 1. Sigma Academy; 2. Sigma OR; 3. Sigma Capacity.  
**Zápis po jednání:** doplnit účastníky, rozhodnutí, vlastníky, termíny a priority.

## 1. Sigma Academy — škálovatelné vzdělávání zdravotníků
**Problém:** Prezenční akademie a workshopy nelze kapacitně škálovat na velké počty zdravotníků.  
**Cíl:** Asynchronní, atraktivní vzdělávání kombinované s praktickými workshopy pro nácvik dovedností.

**Koncept:** krátká videa 3–8 min; interaktivní videa s otázkami; rozvětvené klinické scénáře „co byste udělali?“; krátké testy a zpětná vazba; certifikát o absolvování (nikoli automaticky akreditované kredity); role účastník/lektor/administrátor; mobilní přístup; analytika dokončení a znalostí; pravidelné aktualizace obsahu. Ověřit souhlasy, autorská práva a nepoužívat identifikovatelné pacientské případy bez právního základu.

**Technologické varianty:**
- Moodle LMS + H5P: vhodné pro pilot, evidence průchodu, testy, interaktivní video a větvené scénáře. Ověřit hosting, správu, licence a integraci přihlašování.
- Komerční LMS (např. TalentLMS, LearnWorlds): rychlé nasazení, nutno posoudit cenu na uživatele, export dat, smluvní podmínky a EU hosting.
- Vlastní portál: až při prokázané potřebě specifické UX/integrací; nejvyšší náklady na vývoj a údržbu.

**Doporučený pilot:** 1 kurz / 3–5 mikrolekcí / 1 interaktivní klinický scénář / pretest + posttest / pilotní skupina. Měřit dokončení, čas, změnu znalostí, spokojenost, cenu na proškoleného účastníka. Akreditaci odborného vzdělávání řešit zvlášť.

**K rozhodnutí:** cílové profese a kompetence; první téma kurzu; interní vs. externí prodej; akreditace; vlastník obsahu; produkce videí; rozpočet a hosting.

## 2. Sigma OR — predikce a simulace operačních sálů
**Cíl:** plánovat operační program na základě realistických dob výkonů, personálu a zdrojů, minimalizovat přesčasy, prostoje a rušení; modelovat „co když“.

**Vstupy:** historické operace (typ/kód výkonu, obor, tým, plán/skutečnost, nástup na sál, anestezie, řez, konec, obrat mezi pacienty); elektivní/akutní režim; provozní hodiny sálů; dostupnost operatérů, anestezie, instrumentářek, dospávacích a intenzivních lůžek; přístroje; pravidla priorit. V pilotu používat anonymizovaná/syntetická data.

**Predikce:** nezačínat rigidním rozdělením podle délky; segmentovat podle typu výkonu a variability. Krátké, střední a dlouhé výkony jsou pracovní segmenty, hranice nastavit až z dat. Pro každý výkon predikovat nejen medián, ale i intervaly/kvantily (P50, P80, P90), kalibrovat podle oboru, operatéra a dostupných proměnných. U dlouhých výkonů plánovat riziko překročení konce směny. Validovat časovým rozdělením dat a porovnat proti současnému plánování; sledovat MAE, kalibraci kvantilů a přesčasy.

**Optimalizace:** algoritmus přiřadí výkony do sálů a pořadí s omezeními (kompetence, souběhy, dostupnost týmu, vybavení, pracovní doba, rezervy pro akutní výkony). Optimalizovat vícekriteriálně: počet provedených výkonů, vytížení, čekací dobu, přesčasy a robustnost. Výsledky musí jít ručně upravit a zdůvodnit.

**What-if scénáře:**
1. Přidání dalšího sálu při nezměněném personálu vs. současné posílení týmu.
2. Změna skladby výkonů (více TEP / ortopedie; krátké vs. dlouhé).
3. Prodloužení provozu o hodinu nebo změna rozdělení bloků.
4. Výpadek operatéra / sálové sestry / dospávacího lůžka.
5. Zvýšení rezervy pro akutní případy.
Výstup: Ganttův plán po sálech, srovnání scénářů, očekávané výkony, využití, pravděpodobnost přesčasu, personální a finanční dopady.

**Architektura:** SQL/CSV -> datová validace -> Python (pandas, scikit-learn / gradient boosting pro predikci) -> OR-Tools CP-SAT pro rozvrhování -> simulační vrstva Monte Carlo -> interaktivní aplikace -> Power BI pro následný reporting.

**Volba UI:** Streamlit pro rychlé interní MVP (ovládací prvky, tabulky, grafy); Plotly Dash pro sofistikovanější interaktivní provozní aplikaci; React + FastAPI až pro produkční systém s náročným workflow a uživatelskými rolemi. Power BI ponechat pro KPI, historické porovnání a pravidelný reporting, nikoli jako primární plánovač. Oddělit predikci, optimalizaci a simulaci; jde o různé funkce.

**Pilot:** 1–2 obory, 2–4 sály, historická data alespoň 6–12 měsíců pokud dostupná; nejprve offline backtest, pak paralelní plánování bez zásahu do klinického provozu. Sledovat přesčasové minuty, zrušené výkony, nevyužitý čas, přesnost odhadu a bezpečnostní omezení.

**K rozhodnutí:** dostupnost a kvalita časových značek; definice „využití“ a konce operace; odpovědnost za plán; nejdůležitější scénáře; integrace HIS; pravidla ochrany dat; garant pilotu.

## 3. Sigma Capacity — celonemocniční model kapacit
**Cíl:** propojit plánování operačních sálů s lůžky, JIP, personálem, ambulancemi, zobrazovací diagnostikou, sterilizací a dalšími úzkými místy. Samotné přidání sálu nemusí zvýšit průchodnost, pokud chybí následná kapacita.

**Přístup:** mapovat tok pacienta a návaznosti; modelovat dostupné zdroje a fronty; simulovat příchody, délky pobytů, personální směny a omezení; porovnávat scénáře změn kapacit. Začít návazností sál -> dospávací pokoj/JIP/standardní lůžko; později rozšířit.

**Metody:** diskrétní simulace událostí (např. SimPy), predikce poptávky a délky pobytu, optimalizace rozvrhů (OR-Tools). Výstupy: průchodnost, čekací doby, obsazenost, bottlenecky, náklady, scénáře investic a personálního posílení.

**K rozhodnutí:** které kapacity jsou aktuálně nejkritičtější; vlastnictví dat; první oddělení; cílové KPI; zda stavět jednu sdílenou simulační platformu pro Sigma OR a Sigma Capacity.

## Doporučení napříč tématy
- Vytvořit tři samostatné produktové oblasti se společnou identitou Sigma Care.
- Začít dvěma malými demonstrátory: Academy interaktivní mikrokurz a OR what-if plánovač se syntetickými daty.
- Oddělit analytiku (Power BI) od operačního rozhodování (interaktivní webová aplikace).
- Bezpečnost, GDPR, řízení přístupů, audit a smlouvy o zpracování dat řešit před napojením na reálná nemocniční data. Repozitář je nyní **veřejný**: neukládat sem pacientská data, přístupové údaje ani neveřejné dokumenty.
- Model je nástroj pro podporu rozhodování, nikoli automatická náhrada klinického a provozního schválení.

## Předběžný plán
| Etapa | Výstup |
|---|---|
| Diskuse 22. 10. | Priority, pilotní partneři, vlastníci, kritéria úspěchu |
| Discovery | Inventura dat, procesů, omezení, bezpečnosti |
| Prototypy | Academy 1 modul; OR interaktivní scénáře se syntetickými daty |
| Validace | Pilotní uživatelé, offline ověření, ekonomické zhodnocení |
| Rozhodnutí | Produkční technologie, rozpočet, harmonogram |

## Otevřené otázky / zápis
- Účastníci: TBD
- Rozhodnutí: TBD
- Akční úkoly a vlastníci: TBD
- Termíny: TBD

## Zdroje k technologiím
- H5P větvené scénáře: https://help.h5p.com/hc/en-us/articles/7506761308957-Branching-Scenario-Guide
- OR-Tools: https://developers.google.com/optimization
- OR-Tools scheduling: https://github.com/google/or-tools/blob/stable/ortools/sat/docs/scheduling.md
- Streamlit: https://docs.streamlit.io/get-started/tutorials/create-an-app
- Plotly Dash: https://dash.plotly.com/


## Varianta C – akademická cesta: R + RStudio + Shiny
**Účel:** výzkumně orientované modelování délky operací, statistická validace, simulace a interaktivní what-if scénáře.

**Stack:** R/RStudio; tidyverse/data.table pro přípravu dat; tidymodels, lme4, mgcv a survival pro predikční/statistické modely podle povahy úlohy; simmer pro diskrétní simulaci; ompr/ROI a kompatibilní solver pro optimalizaci; Shiny + plotly pro interaktivní plánování; Quarto a renv pro reprodukovatelnou metodiku.

**Postup:** (1) validace a pseudonymizace dat; (2) statistická explorace a segmentace výkonů podle délky a variability; (3) predikce mediánu i horních kvantilů doby výkonu; (4) diskrétní simulace průchodu operačním programem včetně obratů a akutních případů; (5) optimalizace pořadí výkonů s personálními a časovými omezeními; (6) Shiny dashboard s parametry počet sálů, skladba výkonů/TEP, personál, provozní doba a rezerva; (7) validace na oddělených historických datech a publikovatelná metodika.

**Plusy:** transparentní statistická metodika, dobré prostředí pro akademické publikace, možnost interaktivního prototypu bez samostatného frontendu, otevřený ekosystém. **Rizika:** správa produkčního hostingu Shiny, škálování výpočtů, přístupová práva, integrace do HIS; kvalita optimalizace závisí na zvoleném solveru, nikoli na jazyku R.

**Srovnání:** A = Fabric + Planning (integrované Microsoft prostředí; ověřit aktuální dostupnost/licence); B = Python + vlastní webové UI (flexibilní provozní optimalizace); C = R + Shiny (akademická/statistická cesta). Všechny varianty mohou číst stejný validovaný datový model a publikovat KPI do Power BI. O výběru rozhodnout podle pilotu, bezpečnosti, nákladů a kompetencí týmu.

**Pilot C:** jedna klinika, anonymizovaný/syntetický dataset, predikce P50/P80/P90, 3 scénáře (další sál, více TEP, změna délky provozu), výstup Shiny Gantt + KPI a Quarto metodika. Nejde o automatické klinické rozhodování.
