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
**Odpověď:** _______________________________

### 2. Rozsah datového přístupu
**Otázka:** Jen agregace (A), detailní data (B), nebo reportovací data + povolené detailní analytické funkce (C)?
**Doporučení:** C, read-only, minimální oprávnění, oddělení nemocnic.
**Odpověď:** _______________________________

### 3. Vývojové a produkční umístění
**Otázka:** Azure (A), externí server (B), nebo lokální vývoj na syntetických datech → testovací Azure → produkční Azure (C)?
**Doporučení:** C. Lokální server je vývojový, ne automaticky připojený k nemocničním datům. Vyžádat schválené vývojové nástroje.
**Odpověď:** _______________________________

### 4. Konkrétní pilot
**Otázka:** Které 3–5 kontrol a které existující predikce/metriky použít? Pro koho je výstup?
**Doporučení:** Jeden pilot SigmaCOR, porovnání plán–predikce–skutečnost, odchylky, manažerský komentář; netrénovat nový predikční model.
**Odpověď:** _______________________________

### 5. Zdroj dat pro agenta: datový sklad, Data Lake nebo reportovací soubory?
**Otázka:** Kde jsou skutečně uložené finální KPI, číselníky a predikční výstupy, které už využívá Power BI?
**Doporučení:** Začít konkrétní schválenou výstupní sadou, nikoli přístupem k celému úložišti.
**Odpověď:** _______________________________

### 6. Tok dat a Modeler
**Otázka:** Ukážete jeden úplný tok od zdroje přes pseudonymizaci, OneDrive/ETL, Modeler a datový sklad/Data Lake až po Power BI? Které kroky opravdu probíhají?
**Doporučení:** Nevyvozovat z diagramu neznázorněné vazby Modeleru.
**Odpověď:** _______________________________

### 7. Technické připojení k souborům
**Otázka:** Azure Data Lake – přesný typ, formát CSV/Parquet/Excel, umístění, klíče, verze, autentizace, read-only přístup aplikace; potřebujeme API, nebo lze číst přímo schválené soubory?
**Doporučení:** Pro pilot přímé schválené čtení konkrétních souborů; nové API jen pokud je potřeba stabilní aplikační rozhraní.
**Odpověď:** _______________________________

### 8. Shortcuts a oddělení nemocnic
**Otázka:** Co konkrétně znamenají „Shortcuts Azure Data Lake“ u nemocnice, kde fyzicky data leží, kdo je spravuje a jak jsou odděleni klienti?
**Doporučení:** Prověřit identitu, rozsah oprávnění a audit přístupu.
**Odpověď:** _______________________________

### 9. Frekvence a kvalita
**Otázka:** Diagram uvádí měsíční přenos OneDrive – platí i pro finální metriky a predikce? Jak se pozná dokončená a kompletní dávka?
**Doporučení:** Spouštět po potvrzení dokončení dat, kontrolovat datum, počet řádků, chybějící hodnoty a verzi.
**Odpověď:** _______________________________

### 10. Provoz AI a jazykový model
**Otázka:** Které služby lze schváleně provozovat (Azure Functions/Container Apps/Fabric)? Jaký jazykový model, síťové a cenové limity?
**Doporučení:** Python + schválený model přes API; model není zdroj čísel.
**Odpověď:** _______________________________

### 11. Bezpečnost a právní režim
**Otázka:** Jaký status mají pseudonymizovaná data, kdo je správcem/zpracovatelem, co smí do AI služby, kde běží logy a kdo schvaluje přístup?
**Doporučení:** Pseudonymizovaná data nejsou automaticky anonymní; bez schválení je nedávat do externí AI.
**Odpověď:** _______________________________

### 12. Výstup, schvalování a pravomoci
**Otázka:** Power BI/SigmaCOR, e-mail, aplikace? Smí agent jen číst, nebo něco zapisovat? Kdo schvaluje doporučení?
**Doporučení:** Read-only, fakt → zdroj → hypotéza → doporučení ke schválení.
**Odpověď:** _______________________________

### 13. Testy a akceptace
**Otázka:** Kdo dodá referenční správné výsledky, scénáře a posoudí falešné poplachy a kvalitu komentářů?
**Doporučení:** Testovat výpočty, dohledatelnost, nepodložené závěry, výkon a náklady; syntetická data neprokazují predikční přesnost.
**Odpověď:** _______________________________

### 14. Modeler a Fabric
**Otázka:** Zůstane IBM SPSS Modeler, nebo jej Fabric nahradí? Kde vznikají predikce a jak jsou exportovány?
**Doporučení:** Oddělit AI aplikaci od konkrétní transformační technologie.
**Odpověď:** _______________________________

### 15. Vývoj s Romanem a ChatGPT
**Otázka:** Je povolen AI-asistovaný vývoj, soukromý GitHub, lokální testování a jaké jsou pravidla review, vlastnictví kódu a nasazení?
**Doporučení:** Žádná neveřejná data/tajné klíče do veřejného repozitáře; firemní schválení nástrojů.
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
