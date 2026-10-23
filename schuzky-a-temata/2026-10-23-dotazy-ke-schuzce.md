# SigmaCare – otázky ke schůzce (23. 10. 2026)

## BOD 1 – rozhodnutí o rozsahu řešení (nejprve položit)
**Hlavní otázka:** „Chcete automatické kontroly a komentáře k již vypočteným KPI, nebo interaktivního AI analytika, který na základě dotazu sám vybírá schválené analytické funkce a hledá souvislosti?“

**A – pravidlová automatizace:** předem definované KPI, kontroly kvality a prahové hodnoty, šablony komentářů; Azure Functions nebo Fabric, bez nutnosti LLM. Plus: levnější, předvídatelná, snadno auditovatelná. Minus: neumí ad hoc otázky bez doprogramování.

**Mezivarianta:** výpočty zůstávají deterministické, schválený LLM pouze formuluje shrnutí z ověřených výsledků.

**B – řízený AI analytik:** jazykový model + schválené read-only analytické API, ověřování oprávnění pro každou nemocnici, audit, testování správnosti a nákladů. Plus: nové otázky a flexibilní analýzy. Minus: vyšší integrační, bezpečnostní a provozní složitost. Neumožnit přímý neomezený přístup k datům.

**Doplňující otázky v bodu 1:**
- Kdo je cílový uživatel a co přesně má systém udělat při otevření Power BI?
- Uveďte 3 konkrétní otázky nebo komentáře, které má pilot zvládnout.
- Má AI jen komentovat, také navrhovat hypotézy, nebo i spouštět analýzy? Smí něco zapisovat či měnit?
- Které výsledky musí před publikací schválit člověk?
- Jak poznáme, že pilot uspěl (přesnost, úspora času, uživatelská hodnota)?

**Rozhodnutí ze schůzky:** A / mezivarianta / B / nerozhodnuto

**Poznámky a odpovědi:**

....................................................................................

## BOD 2 – společné technické otázky pro obě varianty
Následující dotazy pokládat u A i B: datový zdroj a výsledné tabulky, aktualizace a dokončení Modeleru, objem a kvalita dat, rozhraní pro čtení, oddělení nemocnic, hosting (Azure/Fabric), výstup do Power BI, odpovědnost za KPI, bezpečnost a audit.

## BOD 3 – doplňující otázky jen pro variantu B
Které schválené analytické nástroje může agent volat? Jak se bude kontrolovat správnost interpretací, přístupová práva, náklady na model, evidence dotazů, bezpečnost promptů a lidské schvalování?

---


## Současné datové toky
1. Kde jsou výsledné reportovací tabulky (Azure Storage, SQL, jiné)?
2. Jak často se data aktualizují a jak je potvrzeno úspěšné dokončení transformací?
3. Běží IBM SPSS Modeler serverově, automaticky, nebo se streamy spouštějí ručně?
4. Jak se ověřuje kvalita, úplnost, čerstvost a původ dat?
5. Jaké části transformací a predikcí se pilotně zkoušejí v Microsoft Fabric?

## Požadovaná funkce
6. Které KPI a odchylky mají být kontrolovány? Kdo schvaluje prahové hodnoty a metodiky?
7. Mají vznikat pouze pravidlové komentáře k hotovým KPI, nebo i interaktivní AI analytik pro ad hoc otázky a hledání souvislostí?
8. Má AI vysvětlovat výsledky, navrhovat hypotézy, nebo autonomně spouštět schválené analytické nástroje?
9. Kde se výstupy zobrazí (Power BI, aplikace, e-mail) a kdo je schvaluje?

## Technická realizace a bezpečnost
10. Je dostupné schválené prostředí Azure Functions, Fabric pipelines/notebooks nebo interní aplikační server?
11. Jaký je objem dat, frekvence zpracování a požadovaná odezva?
12. Jaká rozhraní lze využít pro čtení výsledných dat (SQL/API/soubory)?
13. Jak jsou oddělena oprávnění jednotlivých klientů a řešena identita aplikace, audit a síťové přístupy?
14. Jaké datové kategorie mohou být zpracovány AI a které AI služby jsou smluvně a bezpečnostně schválené?
15. Jak se budou testovat správnost komentářů, falešné poplachy a provozní náklady?

## Rozhodnutí: dvě úrovně řešení
**A – pravidlová automatizace:** načtení schválených reportovacích dat → validace → deterministické výpočty → pravidla/šablony → auditované komentáře. Bez nutnosti LLM. Menší riziko a rychlejší pilot; nevýhoda: omezené na předem definované scénáře.

**B – řízený AI agent:** stejné bezpečné analytické jádro + schválené dotazovací nástroje/API + LLM pro přirozený jazyk, doplňující otázky a interpretaci. Výhoda: flexibilita; nevýhoda: vyšší nároky na bezpečnost, testování, náklady a prevenci chybných závěrů. Agent nemá přímý přístup k celému úložišti ani právo měnit zdrojová data.

**Doporučení:** nejdříve pilot A na jednom reportu, navrhnout API tak, aby se později dalo bezpečně rozšířit o B. Před použitím reálných citlivých dat vyžádat schválení odpovědných osob a ověřit smluvní podmínky.
