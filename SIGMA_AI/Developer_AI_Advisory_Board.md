# Sigma AI — AI vývojový poradní sbor

## Role nástrojů
- ChatGPT / Work: architektura, specifikace, dokumentace a koordinace.
- OpenAI Codex: implementace, refaktoring, testy a návrhy oprav.
- Claude / Claude Code (Anthropic): nezávislé code review, bezpečnostní a logická kontrola, alternativní návrhy.
- GitHub: verzování, issues, Pull Requests, povinné kontroly a historie změn.
- Azure: oddělené vývojové/testovací/provozní prostředí, nasazování a monitoring.

## Standardní postup
1. Vývojář převezme schválené zadání a stanoví akceptační kritéria.
2. Codex pomůže s implementací na samostatné větvi.
3. Spustí se automatické testy, lint, analýza závislostí a skenování tajných údajů.
4. Claude nezávisle zreviduje změny v Pull Requestu (logika, bezpečnost, oprávnění, datové toky, testy, udržovatelnost).
5. Vývojář vypořádá připomínky; u kritických změn následuje další lidská kontrola.
6. Po schválení se změna nasadí nejprve do testovacího prostředí, poté řízeně do produkce.

## Bezpečnostní pravidla
- AI asistenti nemají neomezený přístup k produkčnímu serveru ani k citlivým zdravotnickým datům.
- Pro přístupy se používají minimální oprávnění, krátkodobé identity a auditní logy.
- Žádné produkční klíče ani pacientská data v promptech, GitHub Issues či Pull Requests.
- Před připojením externích AI služeb ověřit smluvní a právní podmínky zpracování dat.
- Dvě AI kontroly nenahrazují lidské schválení, automatické testy ani bezpečnostní audit.

## Licence
Konkrétní tarif ChatGPT/Codex a Claude/Claude Code určit až podle požadované kapacity, limitů, týmové správy a aktuálních obchodních podmínek. Azure a API spotřeba se rozpočtují samostatně.
