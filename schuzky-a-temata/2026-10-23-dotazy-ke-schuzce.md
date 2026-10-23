# SigmaCare – aktualizované otázky a plán pilotu (23. 10. 2026)

**Účel:** pracovní podklad pro hovor, doplňovat odpovědi. **Stav:** návrh, nikoli schválená architektura.

## Co víme z dodaného diagramu Architektura.pdf
- SigmaCare Innovations s.r.o.: Microsoft Cloud Identity & BI Platform, Azure AD B2B, Microsoft 365 Business Premium, SigmaCOR (strategický a operativní reporting), Power BI Desktop, **Datový sklad**, **Azure Data Lake**, OneDrive for Business (SigmaCare Server).
- Nemocnice Nový Jičín: IKIS, DoctIS (SQL), **Shortcuts Azure Data Lake**, OneDrive for Business (SigmaCare Klient), **Pseudonymizace**.
- V diagramu je vyznačeno **ETL** mezi OneDrive SigmaCare a datovým skladem, **měsíční přenos** mezi OneDrive prostředími a **sdílení dat** mezi datovými jezery.
- **Neověřeno:** přesná cesta a umístění výstupů IBM SPSS Modeleru, predikcí a číselníků; aktualizační frekvence jednotlivých sad; zda shortcuts míří na originály nebo kopie; skutečné oprávnění a typ úložiště; provozní Azure pro vlastní aplikace. Pilot Microsoft Fabric je sdělení z diskuse, nikoli součást diagramu.

## Rozhodovací otázky (v pořadí)
### 1. Míra autonomie AI
**Otázka:** Jen definované kontroly (A), samostatný analytik (B), nebo hybrid pravidel a řízených doplňujících analýz (C)?
**Doporučení:** C. KPI a čísla počítat deterministicky, LLM interpretace a schválené analytické funkce, lidské schválení opatření.
**Doptat se:** Co znamená ověřování hypotéz? Jak odlišit fakt, hypotézu a doporučení?
**Praktický příklad:** Pokles využití sálu z 82 % na 64 %: pravidlo označí odchylku, agent prověří schválené souhrny a připraví komentář bez nepodloženého tvrzení o příčině.

**Odpověď:** _______________________________

### 2. Rozsah datového přístupu
**Otázka:** Jen agregace (A), detailní data (B), nebo reportovací data + povolené detailní analytické funkce (C)?
**Doporučení:** C, read-only, minimální oprávnění, oddělení nemocnic.
**Praktický příklad:** Agent vidí agregaci za chirurgii; pro ověření smí získat počet zrušených výkonů podle dne, nikoli otevřít celé pacientské záznamy.

**Odpověď:** _______________________________

### 3. Vývojové a produkční umístění
**Otázka:** Azure (A), externí server (B), nebo lokální vývoj na syntetických datech → testovací Azure → produkční Azure (C)?
**Doporučení:** C. Lokální server je vývojový, ne automaticky připojený k nemocničním datům. Vyžádat schválené vývojové nástroje.
**Praktický příklad:** Roman vyvíjí na 10 000 umělých operacích lokálně, potom stejnou aplikaci nasadí do testovacího a po schválení produkčního Azure.

**Odpověď:** _______________________________

### 4. Konkrétní pilot
**Otázka:** Které 3–5 kontrol a které existující predikce/metriky použít? Pro koho je výstup?
**Doporučení:** Jeden pilot SigmaCOR, porovnání plán–predikce–skutečnost, odchylky, manažerský komentář; netrénovat nový predikční model.
**Praktický příklad:** Plán 100 hodin, predikce 92 hodin, skutečnost 75 hodin: agent porovná hodnoty a připraví manažerský komentář.

**Odpověď:** _______________________________

### 5. Zdroj dat pro agenta: datový sklad, Data Lake nebo reportovací soubory?
**Otázka:** Kde jsou skutečně uložené finální KPI, číselníky a predikční výstupy, které už využívá Power BI?
**Doporučení:** Začít konkrétní schválenou výstupní sadou, nikoli přístupem k celému úložišti.
**Praktický příklad:** Power BI používá soubor utilization_2026_09.parquet; ověřit, zda je v Data Lake nebo skladu a kde leží číselník sálů.

**Odpověď:** _______________________________

### 6. Tok dat a Modeler
**Otázka:** Ukážete jeden úplný tok od zdroje přes pseudonymizaci, OneDrive/ETL, Modeler a datový sklad/Data Lake až po Power BI? Které kroky opravdu probíhají?
**Doporučení:** Nevyvozovat z diagramu neznázorněné vazby Modeleru.
**Praktický příklad:** Představit skutečný tok: nemocniční export → pseudonymizace → přenos → ETL → Modeler → report; pořadí a vazby je nutné potvrdit.

**Odpověď:** _______________________________

### 7. Technické připojení k souborům
**Otázka:** Azure Data Lake – přesný typ, formát CSV/Parquet/Excel, umístění, klíče, verze, autentizace, read-only přístup aplikace; potřebujeme API, nebo lze číst přímo schválené soubory?
**Doporučení:** Pro pilot přímé schválené čtení konkrétních souborů; nové API jen pokud je potřeba stabilní aplikační rozhraní.
**Praktický příklad:** Python čte pouze schválený soubor z konkrétní složky Data Lake pomocí read-only identity; nové API nemusí být nutné.

**Odpověď:** _______________________________

### 8. Shortcuts a oddělení nemocnic
**Otázka:** Co konkrétně znamenají „Shortcuts Azure Data Lake“ u nemocnice, kde fyzicky data leží, kdo je spravuje a jak jsou odděleni klienti?
**Doporučení:** Prověřit identitu, rozsah oprávnění a audit přístupu.
**Praktický příklad:** Shortcut může ukazovat na původní data nemocnice; ověřit, zda agent nemá možnost vidět data jiné nemocnice.

**Odpověď:** _______________________________

### 9. Frekvence a kvalita
**Otázka:** Diagram uvádí měsíční přenos OneDrive – platí i pro finální metriky a predikce? Jak se pozná dokončená a kompletní dávka?
**Doporučení:** Spouštět po potvrzení dokončení dat, kontrolovat datum, počet řádků, chybějící hodnoty a verzi.
**Praktický příklad:** Při neúplném měsíčním přenosu agent čeká na potvrzení dokončení a kontrolu počtu řádků.

**Odpověď:** _______________________________

### 10. Provoz AI a jazykový model
**Otázka:** Které služby lze schváleně provozovat (Azure Functions/Container Apps/Fabric)? Jaký jazykový model, síťové a cenové limity?
**Doporučení:** Python + schválený model přes API; model není zdroj čísel.
**Praktický příklad:** Python vypočítá odchylku, schválený LLM z ověřených hodnot sepíše komentář, nikoli vlastní výpočet.

**Odpověď:** _______________________________

### 11. Bezpečnost a právní režim
**Otázka:** Jaký status mají pseudonymizovaná data, kdo je správcem/zpracovatelem, co smí do AI služby, kde běží logy a kdo schvaluje přístup?
**Doporučení:** Pseudonymizovaná data nejsou automaticky anonymní; bez schválení je nedávat do externí AI.
**Praktický příklad:** Do testu použijeme umělý číselník a agregace; pseudonymizovaný pacientský záznam bez schválení neposíláme do externí AI.

**Odpověď:** _______________________________

### 12. Výstup, schvalování a pravomoci
**Otázka:** Power BI/SigmaCOR, e-mail, aplikace? Smí agent jen číst, nebo něco zapisovat? Kdo schvaluje doporučení?
**Doporučení:** Read-only, fakt → zdroj → hypotéza → doporučení ke schválení.
**Praktický příklad:** Agent navrhne prověřit zrušené výkony, ale sám nemění operační plán; opatření schválí manažer.

**Odpověď:** _______________________________

### 13. Testy a akceptace
**Otázka:** Kdo dodá referenční správné výsledky, scénáře a posoudí falešné poplachy a kvalitu komentářů?
**Doporučení:** Testovat výpočty, dohledatelnost, nepodložené závěry, výkon a náklady; syntetická data neprokazují predikční přesnost.
**Praktický příklad:** Predikce 80 %, skutečnost 60 %, ale chybí polovina dat: agent musí upozornit na neúplnost, ne tvrdit příčinu.

**Odpověď:** _______________________________

### 14. Modeler a Fabric
**Otázka:** Zůstane IBM SPSS Modeler, nebo jej Fabric nahradí? Kde vznikají predikce a jak jsou exportovány?
**Doporučení:** Oddělit AI aplikaci od konkrétní transformační technologie.
**Praktický příklad:** Modeler dnes exportuje predikci do souboru; po případném přechodu na Fabric zůstane pro agenta stejné výstupní schéma.

**Odpověď:** _______________________________

### 15. Vývoj s Romanem a ChatGPT
**Otázka:** Je povolen AI-asistovaný vývoj, soukromý GitHub, lokální testování a jaké jsou pravidla review, vlastnictví kódu a nasazení?
**Doporučení:** Žádná neveřejná data/tajné klíče do veřejného repozitáře; firemní schválení nástrojů.
**Praktický příklad:** Roman s pomocí ChatGPT vytvoří změnu v soukromém GitHubu, provede review a testy; klíče nejsou v repozitáři.

**Odpověď:** _______________________________

## Závěrečný požadavek: co dodat pro pilot
- [ ] Prázdné šablony **skutečných výstupních souborů**: názvy polí, datové typy, klíče, vazby, formáty, časové dimenze.
- [ ] Schválené číselníky nebo bezpečné testovací varianty.
- [ ] Metodika 3–5 KPI a pravidla významných odchylek.
- [ ] Popis jedné existující predikce a výstupních sloupců (predikce/plán/skutečnost).
- [ ] Jeden vzor manažerského komentáře a očekávané výsledky pro 5–10 testovacích scénářů.
- [ ] Mapa konkrétního toku dat, včetně místa Modeleru, Data Lake, datového skladu a Power BI.
- [ ] Popis Azure umístění, formátu, přístupových práv, identity aplikace a aktualizací.
- [ ] Kontaktní osoba pro Azure, datovou metodiku a odbornou akceptaci.
- [ ] Potvrzení schváleného lokálního vývoje, AI nástrojů a testovacího/produkčního nasazení.

**Termíny / odpovědné osoby:** _______________________________

## Navržený pilot s Romanem
1. Získat schéma bez pacientských dat, vytvořit **syntetické CSV/Parquet** a číselníky se stejnými poli; záměrné chyby a odchylky.
2. Lokálně v Pythonu: načtení → validace → porovnání existující predikce/plánu/skutečnosti → pravidla → zdrojově doložený komentář.
3. Testy a odborné ověření; LLM pouze přes schválené rozhraní, bez reálných pacientských dat.
4. Nasadit do **testovacího Azure**, připojit povolenou datovou sadu a ověřit integraci, bezpečnost a skutečné metriky.
5. Teprve po schválení do produkce.

**Rozlišení:** Syntetická data slouží k vývoji a funkčnímu testování, nikoli k prokázání správnosti predikcí na reálném provozu.

## Rychlá pomůcka
**API** = definované rozhraní pro žádosti a odpovědi mezi aplikacemi; není nutné, pokud je schválené přímé čtení souborů. **Azure Data Lake** = úložiště dat; **datový sklad** = připravené analytické datové struktury; **shortcuts** = odkazy na jiná datová umístění, přesný význam zde ověřit; **VPN** = síťová cesta, nikoli oprávnění; **Azure hosting** = místo, kde běží náš kód, nezávislé od otázky, odkud čte data.

## Zápis ze schůzky
**Potvrzený pilot:** __________
**Zdroj metrik/predikcí:** __________
**Technické připojení:** __________
**Vývoj / test / produkce:** __________
**Kontaktní osoby:** __________
**Podklady a termíny:** __________
**Úkoly Roman / já / SigmaCare:** __________

## 16. Způsob používání a integrace AI agenta – NOVÁ ROZHODOVACÍ OTÁZKA
**Hlavní otázka:** „Jak si představujete každodenní použití AI agenta? Má automaticky vytvářet komentáře v SigmaCOR/Power BI, nebo chcete interaktivního asistenta, kterému budou uživatelé pokládat otázky například přes ChatGPT? Nebo obě možnosti?“

**A – Automatický reporting:** plánované spuštění Python analýzy, pravidla a volitelně LLM přes schválené API, výsledek do reportovací tabulky a Power BI/SigmaCOR. MCP není nutné.

**B – Interaktivní analytik:** uživatel se ptá přes schváleného klienta (např. ChatGPT); MCP server zpřístupňuje jen povolené read-only analytické funkce, vrací podložené výsledky. MCP není sám o sobě bezpečnostní tunel ani náhrada přístupových práv.

**C – Obě varianty:** společné Python analytické jádro; automatizační rozhraní (např. REST API nebo plánované dávky) a později MCP pro interaktivní dotazy.

**Doporučení:** C jako cílová architektura, A jako první pilot. MCP doplnit, až bude potvrzený interaktivní scénář, identity a oprávnění.

**Doplňující otázky:**
- Kdo bude uživatelem (management, analytici, nemocnice), odkud se přihlásí a co smí vidět?
- Mají uživatelé pracovat v Power BI, SigmaCOR, ChatGPT, Teams nebo samostatné aplikaci?
- Má být spuštění automatické po aktualizaci dat, na tlačítko, nebo přirozeným jazykem?
- Má být schválené OpenAI API, Azure OpenAI / Microsoft Foundry, nebo vlastní lokálně provozovaný LLM? Jaká data do něj smějí odcházet?
- Kdo bude provozovat a zabezpečovat REST API / MCP server, identity, audit, síťové připojení a oddělení nemocnic?
- Mají se výsledky pouze číst a komentovat, nebo se smí zapisovat do reportovacích výstupů? Jak bude probíhat lidské schválení?

**Požadované podklady navíc:** cílový uživatelský scénář, schválený LLM endpoint a podmínky použití, specifikace integračního rozhraní a identity, cílový report/ukázka uživatelského prostředí, pravidla auditování.

**Rozhodnutí A / B / C:** _______________________________
**Poznámky:** _________________________________________

## 17. MCP hosting a praktické scénáře (pokud zvolí interaktivního agenta)
**Příklad 1:** Manažer: „Proč je využití sálu 67 %, když plán byl 85 %?“ Schválený MCP klient zavolá read-only analytickou funkci v Pythonu, dostane ověřené hodnoty a zdroje; LLM sepíše komentář, nepotvrzené příčiny označí za hypotézy.

**Příklad 2:** „Ukaž tři kliniky s největší odchylkou predikované a skutečné délky operací.“ MCP poskytne jen povolenou funkci, ne přístup k celému Data Lake.

**A – lokální počítač:** vývoj a syntetické testy; neznamená automaticky dostupnost vzdálenému ChatGPT.
**B – Azure SigmaCare:** doporučený produkční hosting, např. Azure Container Apps; vyžaduje schválený HTTPS endpoint, autentizaci, autorizaci, audit a oddělení nemocnic.
**C – externí VPS:** technicky možné, ale vyšší bezpečnostní a smluvní nároky; pouze po schválení.

**Otázky:** Potřebují vzdálený MCP vůbec? Který klient (ChatGPT/Teams/vlastní)? Kde server poběží? Je možné bezpečné síťové připojení klienta? Kdo spravuje Entra ID/OAuth, oprávnění, audit a náklady? Jaká data smí klient a LLM dostat? Které 2–3 read-only analytické funkce se mají vystavit?

**Doporučení:** První pilot bez produkčního MCP; po potvrzení interaktivního scénáře nasadit MCP v Azure SigmaCare. MCP není samo o sobě bezpečnostní tunel.

**Odpovědi / úkoly:** _______________________________
