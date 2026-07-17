# DESIGN.md — receptionistkostnad.se

Vinkel: "vad kostar en receptionist" ägs via en **ledger-kalkylator** — sajten är i grunden ett räkneverktyg, inte en säljsida med en kalkylator påklistrad.

## 1. Brand-identitet

**Färgtokens** (behåll befintliga, utöka med highlight/negative för ledgern):
`--bg:#f4f7f7 --paper:#ffffff --ink:#132420 --ink2:#4f6660 --teal:#0f766e --teal2:#14b8a6 --amber:#d97706 --line:#d9e2e0 --good:#0f766e --line-dash:#c3d1ce`
Ny: `--paper-ruled:#fbfdfc` (subtil ledger-linjering i kalkylator-kortet, repeating-linear-gradient var 28px).

**Typografi**: rubriker i **Georgia** (serif → bokförings-/räkenskapskänsla, skiljer sig från de andra satelliternas rena sans-look), brödtext + UI i `"Segoe UI",system-ui,sans-serif`. Alla kronbelopp `font-variant-numeric: tabular-nums` genomgående (kalkylator, tabell, stats, priskort) — det är den bärande visuella signaturen.

**Ton**: saklig, siffernära, "vi visar räkningen" — inte hajpig. Korta stycken, en avslutande poäng per sektion, inga utropstecken.

## 2. Sektionsplan (topp→ner)

1. **Sticky header** — halvtransparent (`backdrop-filter:blur`), logo + ankare "Kalkylatorn" / "Jämförelse" / "Vanliga frågor" + CTA-knapp "Prova Menodi".
2. **Hero** — H1 clamp(34px,5vw,56px) tight tracking, subline, primär CTA (scrollar till kalkylator) + sekundär CTA ("Se jämförelsen"), 3 trust-chips: "31,42 % arbetsgivaravgift", "12 % semesterlön (schablon)", "Uppdaterad juli 2026". Mockup-plats: produktskärm till höger om rubriken.
3. **Kalkylatorn** — kärnan; behållet JS, tre resultatkort (anställd/svarsservice/AI, AI highlightad), ruled-paper-bakgrund.
4. **Kostnaden post för post** — ledger-tabell (befintlig), highlightad summarad.
5. **Så funkar det** — NY sektion, 3 numrerade steg (01/02/03 + inline-SVG) för hur man går från kalkyl → Menodi live.
6. **Jämförelsetabell** — 3 kolumner (Anställd/Svarsservice/AI) med highlight-rad på AI, kumulativ "vad ingår"-lista.
7. **Stats-band** — endast: arbetsgivaravgift 31,42 % (Skatteverket) + semesterlön 12 % (Semesterlagen) + ev. SCB-medellön kontorspersonal, var och en med källrad. Inga ovverifierade nischsiffror (se STATS-TO-VERIFY.txt — inget godkänt för denna sida ännu).
8. **FAQ (accordion)** — behåll 3 befintliga Q&A, lägg ev. till 1 om bindningstid.
9. **Stor avslutande CTA-band** — behåll, men injicera slider-värdet dynamiskt ("Du kan spara ~X kr/mån").
10. **Flerkolumns-footer** — Kalkylator / Jämförelse / Menodi / Juridik (integritet, källor).

## 3. Vad som BEHÅLLS från nuvarande sida

- Hela kalkylator-JS-logiken (`upd()`, slider 26 000–42 000, formel lön×1,3142 + lön×0,12) — fungerar, återanvänds rakt av, bara omstylad.
- Ledger-tabellen "Kostnaden post för post" med exakta siffror (32 000 / 10 054 / 3 840 / 45 900).
- Alla tre FAQ-svar ordagrant (redan schema.org-taggade, matchar JSON-LD i `<head>` — rör ej texten utan att uppdatera FAQPage-schemat parallellt).
- Juridiskt korrekta procentsatser (31,42 %, 12 %) som enda "stats" tills nischsiffror blir godkända.
- CTA-copy och UTM-länk till menodi.se.

## 4. Mockup-bildplan (placeholders)

- Hero, höger kolumn: skärmdump/mockup av Menodi-kalender som bokar ett möte (16:9, placeholder-ruta med `Mockup: bokningsvy`).
- "Så funkar det": inline-SVG-ikoner per steg (inga fotobilder — konsekvent med feature-grid).
- Jämförelsesektion: liten skärmdump-chip av en SMS-bekräftelse i AI-kolumnen (valfri, low-priority).
- Footer: liten Menodi-logotyp-mark bredvid "en del av Menodi".

## 5. Differentiering mot övriga ~10 satelliter

- Enda sajten byggd **kalkylator-först** — verktyget är hero, inte en sektion.
- Ledger-visuellt språk (linjerat papper, tabular-nums överallt, Georgia-rubriker) — unikt mot de rena sans/teal-varianterna på övriga domäner.
- Personaliserad avslutande CTA som speglar användarens eget slider-värde tillbaka ("du sparar X kr").
- Enda sidan som explicit visar uträkningen (post-för-post), vilket bygger trovärdighet SEO-mässigt kring frågan "vad kostar".
