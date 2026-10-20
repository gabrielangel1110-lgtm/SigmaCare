# Sigma Care – srovnání technologií pro predikci a plánování kapacit
**Podklad k diskusi 22. 10. 2026 | Návrh, nikoli schválené řešení**

| Kritérium | A – Microsoft Fabric | B – Python | C – R (akademická varianta) |
|---|---|---|---|
| Statistický výzkum | Velmi dobrý | Velmi dobrý | Výborný |
| Optimalizace operačního programu | Vlastní algoritmy (např. Python) | Výborná, např. OR-Tools | Dobrá až výborná, dle solveru |
| What-if modelování | Ano, dle implementace | Ano | Ano |
| Interaktivní aplikace | Fabric Planning / další integrace; ověřit dostupnost | Streamlit / Dash | Shiny |
| Akademické publikace | Ano | Ano | Velmi vhodné |
| Produkční nasazení | Silná integrace Microsoft | Flexibilní | Vyžaduje více přípravy |
| Datová vrstva | OneLake / Lakehouse | SQL, Parquet, API | SQL, Parquet, API |
| Významná výhoda | Integrace dat a Power BI | Flexibilní algoritmy a UX | Reprodukovatelná statistika |
| Hlavní omezení | Licence, závislost na ekosystému a limity Planning | Vlastní provoz, zabezpečení a vývoj UI | Provoz Shiny, integrace a škálování |

## Navržená architektura
**A:** Fabric pro data, Python notebooky/modely, Power BI pro reporting, Planning nebo samostatné UI pro scénáře. Dostupnost a licenční podmínky Planning předem ověřit.  
**B:** Python pro predikci (scikit-learn), optimalizaci (OR-Tools), simulaci (např. SimPy) a aplikaci (Streamlit/Dash).  
**C:** R pro statistiku (tidymodels, lme4), simulaci (simmer), optimalizaci (ompr/ROI), Shiny pro scénáře a Quarto pro metodiku.

## Společné scénáře
- Co se stane při přidání dalšího sálu?
- Jak se změní průchodnost při vyšším podílu TEP?
- Jak se změní pravděpodobnost přesčasů při změně personálu nebo délky provozu?
- Jaké úzké místo vznikne na dospávacím pokoji nebo lůžkách?

## Doporučení
Nejdříve pilot s anonymizovanými/syntetickými daty: **Python + interaktivní aplikace (B)** pro provozní prototyp, **R (C)** pro nezávislou akademickou validaci; **Fabric (A)** prověřit jako datovou a reportingovou infrastrukturu podle stávajících licencí. Hodnotit přesnost predikce (včetně kvantilů), přesčasy, vytížení, bezpečnost, provozní náklady a použitelnost.

*Jde o orientační technologické hodnocení, nikoli benchmark nebo ověření aktuálních licenčních podmínek.*
