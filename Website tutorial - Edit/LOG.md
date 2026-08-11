# LOG

Format per regel: datum · wat brak / wat gebeurde er · wat we veranderden ·
welke regel (indien van toepassing, zie friction ladder in `WEBSITE CLAUDE.md`).

---

- **2026-08-12** — `PROFILE.md` en `SKELETON.md` toegevoegd aan het project.
  `WEBSITE CLAUDE.md` herstructureerd naar het SKELETON 9-blokkenformat,
  `PROJECT.md` en dit logbestand aangemaakt. Daarbij een documentatiefout
  gecorrigeerd: de environment-sectie verwees naar een hardcoded pad
  (`C:/Users/nateh/...`) dat niet overeenkomt met dit systeem en ook niet met
  hoe `screenshot.mjs` daadwerkelijk werkt (het zoekt zelf een lokale Chrome/
  Edge-installatie, geen vast puppeteer-pad). Codex CLI/Gemini CLI-orchestratie
  uit SKELETON.md bewust weggelaten — geen accounts daarvoor aanwezig (zie
  `PROFILE.md`).
- **2026-08-12** — Werkmap opgeschoond: alle 97 tijdelijke screenshots in
  `temporary screenshots/` verwijderd (oude iteraties, niet meer nodig). Oude
  `index.html` verplaatst naar `archive/index.html` zodat de root alleen het
  actuele concept (`index-v2.html`) toont.
- **2026-08-12** — Copy-fix: de "Analyse"-kaart in Tools voor dit project
  omschreef zichzelf alsof het de losse Juridische tool was ("Bestemming,
  dubbelbestemmingen en geldende plannen"), terwijl Analyse ook financieel en
  bevindingen bevat. Tekst aangepast.
- **2026-08-12** — Feature: projectinformatie (ingreep + programma) was
  nergens invoerbaar; alle cijfers (bv. "42 appartementen") stonden hard in de
  code. Ontdekt tijdens het uitzoeken: nieuwe projecten hadden sowieso geen
  eigen Projectoverzicht-pagina (`clickable: false`, en de renderfunctie was
  hardgecodeerd aan Kolenkade gekoppeld — negeerde welk project je aanklikte).
  Opgelost: "Nieuw project toevoegen"-modal uitgebreid met ingreep-type en
  programma (woningen/m² GBO/doelgroep); nieuwe projecten zijn nu klikbaar en
  krijgen een eigen (lichtere) Projectoverzicht-pagina met een
  "Projectinformatie"-kaart; Financieel-tool gebruikt nu het ingevulde
  programma i.p.v. verzonnen waarden. Kolenkade blijft de volledige showcase,
  ongewijzigd qua functionaliteit, met dezelfde kaart erbij.
- **2026-08-12** — Feature (op verzoek): linker sidebar uitgebreid. De
  "Project"-sectie was hardgecodeerd op Kolenkade 14-22 en liep daardoor uit
  de pas zodra `activeProject` via een andere weg (Tools-projectkiezer,
  fase-board, kaart) veranderde. Vervangen door "Mijn projecten": een
  doorzoekbare, dynamische lijst van alle `DATA.portfolio`-projecten met
  statusdot (gunstig/aandacht/risico, hergebruikt `portfolioTier`/`tierColor`)
  en inline subnav (Overzicht/Analyse/AI-Chat/Rapport/Samenwerking/
  Stakeholders) onder het actieve project. Alleen projecten met
  `clickable: true` zijn aanklikbaar, wat de bestaande regel respecteert dat
  alleen Kolenkade (en nieuw toegevoegde projecten) een volledig
  Projectoverzicht hebben; de overige seed-projecten tonen grijs/disabled.
  Ook toegevoegd: "Signaleringen"-navitem met live badge (telt nu uit een
  gedeelde SIGNALERINGEN-constante i.p.v. een losse hardgecodeerde "2" op
  drie plekken) die naar het Dashboard springt en naar de
  Signaleringen-kaart scrollt. Breadcrumb voor projectweergaves toont nu ook
  het actieve projectadres i.p.v. altijd "Kolenkade 14-22". Geverifieerd met
  Puppeteer-klikken (projectwissel, zoekfilter, disabled-status,
  signaleringen-navigatie) - geen console-/page-errors.
- **2026-08-12** — Fix + feature (op verzoek): sidebar-accordion sloot niet.
  Het klikken op de header van het al-actieve project riep alleen showView()
  aan, die meteen no-opt als de view al gelijk is (`if (view===currentView)
  return;`) — dus een tweede klik deed zichtbaar niets en de subnav bleef
  altijd open. Root cause: subnav-zichtbaarheid hing af van `currentView`
  i.p.v. een eigen open/dicht-status. Losgekoppeld met nieuwe state
  `sidebarSubnavCollapsed`: header-klik op het actieve project toggled deze
  nu expliciet (met chevron-icoon dat meedraait), navigeren-in-een-project
  (via showView) zet 'm weer open, en het wisselen naar een ander project
  reset 'm naar open. Ook: sidebar "Signaleringen" (scroll-naar-dashboard-
  snelkoppeling) verwijderd — voelde raar aan als los navigatie-item. Ervoor
  in de plaats: een echte nieuwe pagina "Correspondentie" (`data-view=
  "correspondentie"`), een portfoliobreed activiteitenoverzicht dat
  SIGNALERINGEN (portfolioniveau) combineert met de bestaande Kolenkade-
  activiteitenfeed en stakeholder-logs — bedoeld als bredere, portfolio-
  schaal variant van de bestaande project-Samenwerking-pagina. Dashboard
  Signaleringen-kaart/KPI ongewijzigd gelaten. Geverifieerd met Puppeteer
  (toggle-gedrag, correspondentie-item count) - geen console-/page-errors.
