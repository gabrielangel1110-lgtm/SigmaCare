# První zadání od Petra Maška – portfolio AI agentů SigmaCare
**Datum evidence:** 22. 10. 2026  
**Zdroj:** text zprávy od Petra Maška předaný v konverzaci  
**Stav:** návrh k projednání, nikoli schválená implementace

> Ahoj Gabčo,  
> Posílám slíbený text, za mne vidím prioritu v SigmaCOR Process Analyst a SigmaHEART Analyst.  
> V klidu si to projdi a pojďme si k tomu zavolat.  
> Měj se, Petr

## 1. Doporučené portfolio AI agentů
Priority jsou návrhem podle potenciálního přínosu a návaznosti na současné projekty, nikoli výsledkem finančního výpočtu návratnosti.

| AI agent | Co by dělal | Potenciál | Priorita |
|---|---|---|---|
| SCI Project Manager | Hlídání projektů, termínů, závazků, zápisů a úkolů | Interní úspora času | Velmi vysoká |
| SCI Data Quality Agent | Automatická kontrola nemocničních dat, hledání anomálií | Interní i klientská hodnota | Velmi vysoká |
| SCI DRG Expert | Metodiky CZ-DRG, číselníky, vykazování, validace | Odborná efektivita | Velmi vysoká |
| SigmaCOR Process Analyst | Průběžná identifikace procesních ztrát | Nová funkce produktu | Velmi vysoká |
| SigmaCALC Economic Analyst | Ekonomické odchylky hospitalizací, vysvětlení nákladů | Nová funkce produktu | Vysoká |
| SigmaHEART Analyst | Hodnocení trendů, materiálu a kapacit kardiocenter | Nová funkce produktu | Vysoká |
| SCI Lean Coach | Podpora projektů DMAIC a Kaizen | Konzultační škálování | Vysoká |
| SCI Knowledge Agent | Interní znalostní báze metodik, projektů a postupů | Zachování know-how | Vysoká |
| SCI Sales & Proposal Agent | Příprava nabídek, smluvních podkladů a obchodních návazností | Interní úspora času | Střední |
| SCI Academy Tutor | Personalizovaná výuka a testování lékařů | Nový vzdělávací produkt | Střední |

Petr dále píše: „Začal bych prvními třemi a současně navrhl pilot jednoho agenta přímo do produktu SigmaCOR nebo SigmaCALC.“ V úvodním e-mailu ovšem výslovně označuje za priority SigmaCOR Process Analyst a SigmaHEART Analyst. **Pořadí pilotů je třeba na hovoru vyjasnit.**

## 2. Konkrétní příležitosti

### A. Interní agenti – rychlé výsledky

**SCI Project Manager:** přístup k vybraným projektovým prostorům Teams, Planner, SharePoint, případně Outlook; zápisy, návrhy úkolů, kontrola termínů, nevyřešené závazky. Příklad: přehled projektu Dräger za poslední dva týdny. Týdenní souhrn aktivních projektů SigmaCare; zápis nebo změna úkolů až po schválení.

**SCI Data Quality Agent:** syntaktické a sémantické kontroly, porovnání datových dávek s historií, anomálie ve výkonech, ZUM, pracovištích a časech, nálezy dle závažnosti, možné příčiny a otázky pro nemocnici. Příklad: více případů na intervenčním sále bez vykázaného materiálu. Deterministické kontroly zůstanou v SQL, SPSS nebo Pythonu; AI interpretuje a prioritizuje.

**SCI DRG Expert:** verzované metodiky CZ-DRG, klasifikace, číselníky a validační postupy; vždy uvede verzi a konkrétní pravidlo, rozliší prokázaný rozpor od podezření a připraví podklad pro odborné posouzení. Příklad: kombinace výkonu, ZUM a zařazení hospitalizace dle pravidel 2026.

### B. Produktoví agenti – strategická příležitost

**SigmaCOR Process Analyst – agent procesní výkonnosti:** podle Petra nejlepší kandidát na první produktový pilot. Týdenní analýza operačních sálů a pacientské cesty, odchylky a hypotézy o příčinách. Ilustrativní příklad: pokles využití sálů o 6 procentních bodů proti předchozím čtyřem týdnům, možný vliv pozdějších začátků a delších obratů. Doporučit prověřit připravenost pacienta, anesteziologický tým a úklid. **Příklad je fiktivní; příčiny musí být ověřeny.**

**SigmaCALC Economic Analyst:** neobvyklé náklady nebo výsledky hospitalizací a DRG skupin; rozklad faktorů ZUM, lůžkové péče, operačního času a skladby případů. Možné propojení s daty o nozokomiálních infekcích od Datlowe; neinterpretovat asociaci jako prokázanou kauzalitu.

**SigmaHEART Analyst:** trendy počtu a struktury výkonů, specifického materiálu, využití intervenčních sálů a lůžek, odchylky od projekcí. Příklad: růst TAVI nad projekci a dopady na materiál, kapacity a očekávané náklady. Společné vyhodnocení klinických, procesních a ekonomických dat.

## 3. Architektura navržená Petrem
1. **Nemocniční zdroje:** NIS, výkony, ZUM, DRG, časová razítka, ekonomická data.
2. **Validovaná analytická vrstva SigmaCare:** SQL, transformace, kontroly, Power BI modely, metodiky KPI.
3. **Specializovaný AI agent:** odchylky, ověřování, interpretace, návrhy opatření.
4. **Manažerská zpráva:** co se změnilo a proč to prověřit.
5. **Návrhy opatření:** ke schválení odpovědnou osobou.

Výpočty mají být reprodukovatelné a AI má interpretovat výsledky a formulovat hypotézy, nikoli nahrazovat validované výpočty.

## 4. Návrh dalšího postupu – pracovní doplnění procesní analýzy (nikoli Petrův text)
- Na hovoru potvrdit, zda první produktový pilot bude **SigmaCOR** nebo **SigmaHEART**; vyjasnit rozpor mezi úvodní prioritou a doporučením začít interními třemi agenty.
- Pro vybraný pilot definovat uživatele, 5–10 konkrétních otázek, vstupní KPI, jejich přesné definice, datové zdroje a přípustné interpretace.
- Připravit akceptační testy: správnost výpočtů, srovnávací období, vysvětlitelnost nálezu, zdroj každého tvrzení, falešné poplachy a schvalování opatření.
- Pro první demo použít syntetická data. Přístup ke skutečným nemocničním datům až po schválení zabezpečení a oprávnění.
- Role k potvrzení: Petr – produktové priority; Gabriela – procesní analýza a QA; Roman – implementace; Lukáš – datová architektura.

**Poznámka:** V tomto veřejném repozitáři je pouze pracovní shrnutí zadání bez podpisových kontaktních údajů a bez nemocničních dat. Přístupová oprávnění a důvěrnost případných dalších podkladů je nutné řešit samostatně.
