# CLAUDE.md — Planinzicht (Website Project)

## 1. Context & goal
Zie `PROJECT.md` voor het volledige projectdoel. Kort: "Planinzicht" is een
intern dashboard/portaal voor bouw- en vastgoedprojecten, voor projectleiders/
adviseurs. `index-v2.html` is het actuele concept.

## 2. Role & scope of the lead
De Claude-sessie is **lead en orchestrator** van dit project, niet de enige
uitvoerder. Taken: instructies lezen, beslissingen nemen, werk delegeren aan de
juiste skill/agent, resultaten reviewen, fouten herstellen, het systeem
verbeteren. Niet alles zelf proberen te doen.

## 3. Always do first
- Lees `PROFILE.md`, `SKELETON.md`, `PROJECT.md` en `LOG.md` voor je begint.
- **Invoke the `frontend-design` skill** before writing any frontend code,
  every session, no exceptions.

## 4. Environment
- **OS:** Windows.
- **Server:** `node serve.mjs` — serveert de projectroot op
  `http://localhost:3000`. `serve.mjs` staat in de projectroot. Start hem op de
  achtergrond vóór je screenshots maakt. Draait de server al, start dan geen
  tweede instantie.
- **Screenshots:** `node screenshot.mjs http://localhost:3000 [label]`.
  `screenshot.mjs` gebruikt `puppeteer-core` en zoekt zelf een lokaal
  geïnstalleerde Chrome of Edge (`C:/Program Files/Google/Chrome/...` of
  `.../Microsoft/Edge/...`) — geen vast gebruikerspad nodig. Screenshots komen
  automatisch (auto-genummerd, nooit overschreven) in
  `./temporary screenshots/screenshot-N[-label].png`.
- **Nooit** een `file:///`-URL screenshotten — altijd via localhost.
- Lees de PNG na het maken met de Read-tool om het beeld te analyseren.

## 5. Capability register (project-local view)
- **Skill `frontend-design`** — verplicht vóór elke frontend-wijziging.
- **`serve.mjs` / `screenshot.mjs`** — lokale dev-server en screenshot-tool,
  gebruik as-is, niet herschrijven zonder reden.
- Nieuwe skills/MCP's/agents worden aan Melle voorgesteld en pas na
  goedkeuring geïnstalleerd (zie `PROFILE.md`).
- Codex CLI / Gemini CLI zijn **nog niet beschikbaar** in dit project (geen
  accounts) — niet aannemen dat werk daarnaartoe gedelegeerd kan worden totdat
  dat verandert.

## 6. Working loop — with a verification gate
Elke taak volgt: poging → **verifiëren tegen grond-waarheid** → fix →
opnieuw verifiëren → pas stoppen bij een duidelijke stopconditie (niet na één
pas).

**Referentiebeelden:**
- Bij een referentiebeeld: layout, spacing, typografie en kleur exact matchen.
  Placeholder-content gebruiken (`https://placehold.co/`, generieke tekst).
  Niet verbeteren of toevoegen aan het ontwerp.
- Zonder referentiebeeld: ontwerp from scratch met hoge kwaliteit (zie
  anti-generic guardrails hieronder).
- Screenshot maken, vergelijken met referentie, verschillen fixen, opnieuw
  screenshotten. Minimaal 2 vergelijkingsrondes. Pas stoppen als er geen
  zichtbare verschillen meer zijn, of Melle het zegt.

**De friction ladder** (zie `PROFILE.md` voor de achtergrond):
- Pogingen 1–2: normaal proberen.
- Na 2 mislukkingen op hetzelfde probleem: stop met varianten proberen. Zoek
  grond-waarheid op — echte DOM, screenshot, console-output, logs.
- Na 3: wissel van tool/agent. Actief zoeken of er een skill/MCP/agent bestaat
  voor dit exacte probleem.
- Na 4: terugkomen bij Melle met een korte samenvatting van wat geprobeerd is
  en **twee concrete opties** — niet blijven doorgaan.
- Elke keer dat dit vuurt: loggen in `LOG.md`.

**De review gate:**
- Geen resultaat van een externe agent/sub-agent wordt geaccepteerd zonder dat
  de lead het eerst controleert op fouten.

## 7. Output defaults
- Eén `index.html`-bestand, alle styles inline, tenzij Melle iets anders zegt.
- Tailwind CSS via CDN: `<script src="https://cdn.tailwindcss.com"></script>`.
- Placeholder-afbeeldingen: `https://placehold.co/WIDTHxHEIGHT`.
- Mobile-first responsive.

## Brand Assets
- Altijd de `brand_assets/`-map checken vóór het ontwerpen (nog niet aanwezig
  in dit project — indien die later verschijnt, gebruik echte assets in plaats
  van placeholders, en gebruik het gedefinieerde kleurenpalet/logo indien
  aanwezig).

## Anti-Generic Guardrails
- **Colors:** nooit het default Tailwind-palet (indigo-500, blue-600, etc.).
  Kies een custom merkkleur en leid daarvan af.
- **Shadows:** nooit een platte `shadow-md`. Gebruik gelaagde, kleur-getinte
  shadows met lage opacity.
- **Typography:** nooit hetzelfde font voor headings en body. Combineer een
  display/serif met een clean sans. Tight tracking (`-0.03em`) op grote
  headings, ruime line-height (`1.7`) op body.
- **Gradients:** meerdere radial gradients gelaagd. Grain/textuur via SVG
  noise-filter voor diepte.
- **Animations:** alleen `transform` en `opacity` animeren. Nooit
  `transition-all`. Spring-achtige easing.
- **Interactive states:** elk klikbaar element heeft hover-, focus-visible- en
  active-states. Geen uitzonderingen.
- **Images:** gradient overlay (`bg-gradient-to-t from-black/60`) en een
  kleurbehandeling met `mix-blend-multiply`.
- **Spacing:** intentionele, consistente spacing-tokens — geen willekeurige
  Tailwind-stappen.
- **Depth:** surfaces hebben een laagsysteem (base → elevated → floating), niet
  allemaal op hetzelfde z-vlak.

## 8. Hard rules
Autonomiegrenzen uit `PROFILE.md` — **altijd** eerst goedkeuring van Melle
voor:
- committen
- pushen
- deployen
- betaalde API-calls / iets dat credits kost
- bestaande bestanden overschrijven of verwijderen
- `rm` of andere destructieve bestandssysteem-operaties

Project-specifieke hard rules:
- Geen secties, features of content toevoegen die niet in de referentie staan.
- Een referentie-ontwerp niet "verbeteren" — matchen.
- Niet stoppen na één screenshot-pas.
- Geen `transition-all` gebruiken.
- Geen default Tailwind blue/indigo als primaire kleur.

## 9. Log & retro protocol
- **Tijdens het project:** elke beslissing, elke breuk, elke fix toevoegen aan
  `LOG.md` — datum, wat brak, wat we veranderden, welke regel (indien van
  toepassing) het opleverde.
- **Aan het eind:** de aangepaste `CLAUDE.md` + `LOG.md` teruggeven aan het
  meta-project voor een retro; lessen die in twee projecten terugkomen worden
  bevorderd tot een vaste regel in `SKELETON.md`/`PROFILE.md`.
