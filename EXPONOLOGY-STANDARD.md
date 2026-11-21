# Exponology Page Standard — DRAFT

**Purpose:** every Learn page and every app page follows one common format, so a new app can be built to the standard without back-and-forth. When a page and this standard disagree, the standard wins; fix the page.

**Scope:** the home page, all Learn pages (`/apps/<app>/`), and all app pages (`/apps/<app>/app.html`). The standard covers layout, menus, header, colors, fonts, section headers, and content (what goes where, and what must not be repeated).

**Status:** DRAFT — written from an audit of the live site on 2026-11-07. Not yet approved by Mike. The divergence list in §6 is the work needed to bring existing pages into line.

---

## 1. Shared tokens — one set, used everywhere

Every page uses the same CSS custom properties. Do not invent new hex values. If an app needs an accent that is not in this list, add it as a documented exception in §1.3 and use the shared tokens for everything else (background, ink, lines, radius).

### 1.1 Colors (light)

| Token | Value | Use |
|---|---|---|
| `--bg` | `#faf8f2` | Page background |
| `--bg-deep` | `#173f2c` | Dark-green closing panel, deep sections |
| `--surface` | `#ffffff` | Cards, panels |
| `--surface-soft` | `#f1ede1` | Soft panels, alternate rows |
| `--ink` | `#1e2b23` | Body text, headings |
| `--ink-soft` | `#48584e` | Secondary text |
| `--ink-faint` | `#71806f` | Tertiary text, captions |
| `--line` | `#ddd6c4` | Borders, rules |
| `--green` | `#1f6f4a` | Primary green (links, accents) |
| `--green-strong` | `#17573a` | Green hover / strong |
| `--green-soft` | `#e3efe6` | Green tint background |
| `--red` | `#b23a2e` | Red accent (eyebrow dash, warnings) |
| `--red-soft` | `#f7e3df` | Red tint background |
| `--gold` | `#a97b16` | Gold accent (App No. pill, highlights) |
| `--gold-soft` | `#fbf0cd` | Gold tint background |
| `--on-deep` | `#f3efe3` | Text on dark green |
| `--on-deep-soft` | `#c9d6c6` | Secondary text on dark green |
| `--shadow` | `0 18px 44px rgba(23,63,44,.14)` | Card shadow |
| `--radius` | `14px` | Card/panel corner radius |

### 1.2 Fonts

- **Body / UI:** `"Public Sans", system-ui, -apple-system, sans-serif`. Body font-size `17px`.
- **Headings:** `"Newsreader", Georgia, serif`.
- **Line-height:** `1.6` for prose (Learn pages, home page, Help text). `1.45` for compact app UI (controls, cards, lists) only.
- **h1:** Newsreader, `font-size: clamp(38px, 6vw, 58px)`, `line-height: 1.06`, `font-weight: 600`, `letter-spacing: -.015em`, `margin: 16px 0 14px`.
- **h2:** Newsreader, `font-size: clamp(28px, 4.2vw, 38px)`, `line-height: 1.15`, `font-weight: 600`, `letter-spacing: -.01em`, `margin: 0 0 8px`.
- **Eyebrow:** small caps, red dash before it (`::before`), green text. One line.

### 1.3 Documented exceptions (the only allowed deviations)

| App | Exception | Why |
|---|---|---|
| CipherDesk (app only) | Dark-only theme (`color-scheme: dark`; `--bg: #10160f`, `--paper: #1a211a`, `--ink: #edeae0`, `--accent: #7bc79b`, `--gold: #d8ab4e`). | Mike's ruling: CipherDesk is dark-only. The Learn page still uses the shared light tokens. |
| Mah Jongg Hand Finder & Learning Game (apps only) | Jade accent instead of green: `--jade: #145c43`, `--jade-strong: #0e4a35`, `--jade-soft: #e2ede6`; red `#a61e14`; gold `#8a6d1b`. | Mah Jongg identity (jade/red/gold tiles). Layout tokens (`--bg`, `--ink`, `--line`, `--radius`, margins) still follow §1.1/§1.2. |
| The Mah Jongg Learning Game Learn | Extra tokens `--brown: #8a5a2b`, `--joker: #6d28d9`, `--joker-soft: #efe9fd` (tile/joker colors in diagrams). | Diagram colors only. |

No other per-page hex values. No per-page font stacks. If a new app needs an accent, add it here first, then use it.

### 1.4 Margins and width

- **Wrap:** `.wrap { max-width: 1080px; margin: 0 auto; padding: 0 22px; }` on every page. No page uses a different max-width or side padding.
- **App pages:** the wrap also carries `padding: 20px 22px 48px` (20px top, 48px bottom). The page content sits inside `.wrap`.
- **Learn pages and home page:** `.wrap` is `padding: 0 22px`; the hero/header supplies the top spacing and the footer supplies the bottom spacing.
- **No other margin mechanism.** Do not set page margins with body padding or a `--page-max` variable; use `.wrap`.
- **Same-tab navigation everywhere.** No `target="_blank"`, no `window.open`. Every visible "Exponology" text links to `https://exponology.com/`.

---

## 2. Learn pages (`/apps/<app>/`)

A Learn page teaches the app. It does not do the app's job.

### 2.1 Top menu (common, same on every Learn page)

Order, left to right:

1. **Wordmark** — "Exponology." (Newsreader, red dot) with "exponology.com" underneath. Links to `https://exponology.com/`. Turns green on hover.
2. **Section links** — the page's own sections, in page order, short labels (e.g. "The map", "The sheet", "Matching", "The board"). These are the ONLY page-specific links allowed in the top menu. Each links to its section anchor (`#map`, `#sheet`, …).
3. **Apps dropdown** — button labeled "Apps". Lists **every live app, in home-page order**, each linking to that app's **app page** (`/apps/<app>/app.html`). The current app is marked "You are learning this one". The dropdown must be kept in step with the home page: when a new app goes live, add it to every Learn page's Apps dropdown and to the home page's Apps dropdown at the same time.
4. **Open button** — "Open \<App name\>" (e.g. "Open CipherDesk"), linking to the app page. One button, same label pattern on every Learn page.

Nothing else in the top menu. No Help link in the header (Help links live beside section headings — see §2.4). No social links, no extra buttons.

### 2.2 Header

- **Eyebrow (required, one line):** the app's identity in a few words — a count or a tagline, e.g. "71 quotes · 9 categories", "2026 Card · 79 Hands", "Match loose pieces to the map". Never empty, never missing.
- **H1:** one sentence, what the app does for the user (e.g. "Fill in the blanks, one letter at a time."). Newsreader, per §1.2.
- **Lede:** one short paragraph (max ~200 characters) saying what the app does. It must NOT explain how the app works — that is what the sections below are for (§5, content rule).

### 2.3 Sections

- **First h2 is always "The app, at a glance"** — a short overview with the app's real screenshots (never rebuilt graphics) and the steps in brief.
- **Then one section per step or per idea**, in the order the user does them. Numbered steps use a "1. ", "2. " prefix (e.g. "1. Set up the map"). Unnumbered sections (e.g. "How to read a piece card") go where they belong in the flow, not in a separate area.
- **h2 style** per §1.2. Section headings are Newsreader, not bold body text.
- **Screenshots are real screenshots of the app itself** — nothing redrawn, nothing rebuilt. Say so on the page if it helps, but do not claim a picture is a screenshot when it is not (e.g. a labeled format diagram must be labeled as a format example, not a screenshot).
- **Closing section (`class="closing"`, dark green, `--bg-deep`):** the last section on the page. It carries an **App No. pill** — "App No. N · Exponology" (gold pill on dark green) — where **N is the app's number on the home page**, and a paragraph that names the app's place in order (e.g. "CipherDesk is one of the apps on the Exponology home page — App No. 3, after The Mah Jongg Hand Finder (App No. 1) and The Mah Jongg Learning Game (App No. 2) and before Prime Factor Finder (App No. 4)."). App names and numbers must match the home page exactly. Every Learn page has a closing panel with an App No. pill; no Learn page omits it.

### 2.4 Help links

- Each section's Help link goes to **that section's Help inside the app** (e.g. `#help-map`, `#help-sheet`). The link sits beside the section heading, not in the header and not in a separate Help section on the Learn page.
- Every section that has a matching Help section in the app gets a Help link. If a section has no matching Help in the app, it gets no Help link (do not link to a generic Help).

### 2.5 Footer (Learn pages)

- Wordmark link to `https://exponology.com/`.
- A link to the app ("\<App name\>" → the app page).
- "exponology.com" link.
- The site tagline: "— small apps, developed with the help of AI, born from everyday frustrations."
- **No "(prototype)"** in the footer once the app is live. Remove the word when the app publishes.

---

## 3. App pages (`/apps/<app>/app.html`)

An app page does the job. It does not re-teach the Learn page.

### 3.1 Header (same standard header as the Learn pages)

- **Brand bar:** `brand-bar` / `brand-home` / `brand-logo` / `brand-sub` — the stacked wordmark "Exponology." (Newsreader, red dot) with "EXPONOLOGY.COM" underneath, linking home, turning green on hover. Same markup on every app page. (CipherDesk is the one exception to the markup — see §6 — and must be brought into line or recorded as a deliberate exception.)
- **Eyebrow (required, one line):** same identity line as the Learn page (e.g. "71 quotes · 9 categories", "2026 Card · 79 Hands"). It is the same text on the app and its Learn page.
- **H1:** the app's name (e.g. "Prime Factor Finder", "CipherDesk", "Jigsaw Piece Finder"). Newsreader, per §1.2.
- **Lede:** one short paragraph (max ~200 characters) saying what the app does. It must NOT explain how it works — that belongs in the Help (§3.3) and the Learn page. If the lede is longer than ~200 characters, shorten it.

### 3.2 Menus

- **App pages have no top navigation menu** beyond the wordmark (home link). There is no Apps dropdown on an app page and no section nav in the header. Navigation inside the app is the app's own controls (steps, tabs, buttons), not a site menu.
- **Help links** sit beside section headings (see §3.3), not in the header.

### 3.3 Sections and Help

- **Section h2s** are the app's steps or areas, in the order the user does them (e.g. "Set up the map", "Photograph a sheet of pieces", "Match the pieces", "Where things stand"). Numbered steps use a "1. ", "2. " prefix when the sections are a sequence (as in Prime Factor Finder). h2 style per §1.2.
- **Help is always the last h2 on the page**, titled "Help". It has the approved 2-section layout (the Hand Finder Help layout is the pattern): two sections at the bottom, Help links in a few places beside section headings, NOT in the header.
- **Help answers how-to in the app.** It does not repeat the Learn page. If the Learn page already explains a concept, the Help says how to do it in the app and links to the Learn page — it does not paste the Learn page's explanation.

### 3.4 Footer (app pages)

- Wordmark link to `https://exponology.com/`.
- **One line** saying what the app is (not how it works, not a repeat of the Help). Example: "Prime Factor Finder is one of the learning apps at Exponology — exponology.com."
- **No "work in progress" / "prototype" / "first pass" wording once the app is published with a Learn page.** Caveats about accuracy belong in the Help (one place), not in the footer. Remove stale status words when the app publishes.
- Reference information that the user needs while using the app (e.g. the Mah Jongg notation key) lives in the Help, not in the footer. The footer is one line, not a reference card.

### 3.5 Colors, fonts, margins (app pages)

- Same shared tokens (§1.1), same fonts (§1.2), same `.wrap` (§1.4). Per-app accents only as documented in §1.3.
- Body font must include `"Public Sans"` in the stack. Do not use a system-only sans stack.
- Body line-height `1.45` for compact app UI; prose inside Help uses `1.6`.

---

## 4. Home page (`/`)

- **Top menu:** wordmark + "The Idea", "Apps" dropdown, "How They're Built", "Founder Note", "What's Next". The Apps dropdown lists **every live app, in card order**, linking to each app's card anchor (`#app-<slug>`).
- **App cards:** one card per live app, in order, each with an "App No. N" label, the app name, a one-line tagline, an "Open" button (to the app) and a "Learn More" button (to the Learn page). Card order defines the App No. used on every Learn page (§2.3). When a new app goes live, add its card here **and** add it to every Apps dropdown (home page + all Learn pages) at the same time.
- **Current card order (verified 2026-11-07):** No. 1 The Mah Jongg Hand Finder, No. 2 The Mah Jongg Learning Game, No. 3 CipherDesk, No. 4 Prime Factor Finder. (Jigsaw Piece Finder is live with a Learn page but has no home-page card yet — see §6.)
- **Footer:** wordmark link home, a few links, the site tagline, "exponology.com".
- Same tokens, fonts, and `.wrap` as §1.

---

## 5. Content rule — do not repeat, combine where possible

This is the rule that does the most work. Apply it to every page, old and new.

1. **Each fact lives in exactly one place.** The Learn page teaches it, the app does it, or the Help explains how to do it in the app — pick one home and link to it from the others. Do not paste the same explanation in two places.
2. **The lede is not a manual.** One short paragraph (max ~200 characters) saying what the app does. How it works belongs in the sections (Learn page) or the Help (app page), not in the lede.
3. **The footer is not a reference card.** One line. Reference material (notation keys, matching criteria, caveats) lives in the Help or the Learn page, not in the footer.
4. **If two apps share reference info, write it once.** Put the full text in the one place it belongs (the relevant Learn page or Help) and link to it from the other app. Do not paste the full text in two footers or two Help sections.
5. **Combine sections that say the same thing.** If two sections (on the same page or across the Learn page and the app Help) explain the same idea, merge them into one section and link to it. Do not keep both with slightly different wording.
6. **Status words expire.** "Prototype", "work in progress", "first pass", "coming soon" are removed the day the app publishes with a Learn page. A caveat that is still true after publishing belongs in the Help (one place), phrased as what to check, not as a status label.
7. **Names and numbers match the home page.** App names, App No., and card order are taken from the home page (§4). A Learn page or app page that names another app must use the home page's name and number for it.
8. **Screenshots are real.** A Learn page shows real screenshots of the app. A diagram that is not a screenshot must be labeled as what it is (e.g. "format example"), not presented as a screenshot.

---

## 6. Divergence list — what each existing page must change to conform

Audited 2026-11-07 against the live site (repo `~/workspace/exponology-site`, commits through `612cada`). "Must change" means the page breaks the standard; "Consider" means it follows the letter but could be tightened.

### 6.1 Home page (`index.html`)

- **Must change:** Apps dropdown lists only 4 apps — Jigsaw Piece Finder is missing. Add it (and add a Jigsaw card as App No. 5, or decide Jigsaw has no home-page card and remove the "App No. 5" pill from the Jigsaw Learn page — the two must agree, §2.3/§4).
- **Must change:** No Jigsaw card. The Jigsaw app is live with a Learn page; either add its card as App No. 5 or record a deliberate decision that it stays off the home page (and then the Jigsaw Learn page must not claim App No. 5).
- Otherwise conforms (tokens, fonts, `.wrap`, footer, card order 1–4 correct).

### 6.2 Prime Factor Finder Learn (`apps/factor-finder/index.html`)

- **Must change:** No Apps dropdown in the top menu. Add it (all 5 apps, in home-page order, Prime Factor Finder marked "You are learning this one").
- **Must change:** No App No. pill in the closing panel. Add "App No. 4 · Exponology" and the closing paragraph naming its place (after CipherDesk No. 3, before Jigsaw No. 5 — or before Prime Factor Finder is last if Jigsaw has no card; must match the home page).
- **Must change:** Footer still says "Prime Factor Finder (prototype)". Remove "(prototype)" — the app is live.
- Otherwise conforms (tokens, fonts, `.wrap`, eyebrow, h1/h2, section Help links, Open button).

### 6.3 CipherDesk Learn (`apps/cipherdesk/index.html`)

- **Must change:** Apps dropdown lists only 4 apps — Jigsaw Piece Finder is missing. Add it (in home-page order, after Prime Factor Finder).
- Otherwise conforms (tokens, fonts, `.wrap`, eyebrow, h1/h2, closing panel App No. 3 with correct names/order, Help links, Open button, footer). This is the closest to the standard; use it as the reference Learn page (after the Apps dropdown fix).

### 6.4 The Mah Jongg Learning Game Learn (`apps/mah-jongg-hand-matcher/index.html`)

- **Must change:** No Apps dropdown in the top menu. Add it (all 5 apps, in home-page order, Learning Game marked "You are learning this one").
- **Must change:** No eyebrow. Add one (same identity line as the app: "2026 Card · 79 Hands").
- **Must change:** No App No. pill in the closing panel. Add "App No. 2 · Exponology" and the closing paragraph naming its place.
- **Must change:** Footer still says "Hand Matcher (prototype)". Remove "(prototype)" — the app is live.
- **Must change:** No Help links (0 `#help-` links). Add a Help link beside each section heading that has a matching Help section in the app.
- **Must change:** Open button label is "Try the Matcher". Rename to "Open The Mah Jongg Learning Game" (the §2.1 label pattern).
- Otherwise conforms (tokens — plus the documented extra `--brown`/`--joker` tokens — fonts, `.wrap`, h1/h2).

### 6.5 Jigsaw Piece Finder Learn (`apps/jigsaw-piece-finder/index.html`)

- Conforms on the top menu (Apps dropdown with all 5 apps, current app marked), eyebrow, h1/h2, Help links (4), Open button, footer, and closing panel (App No. 5).
- **Must change (conditional):** The App No. 5 pill assumes a home-page card as No. 5. If the home page does not add a Jigsaw card, remove the pill (see §6.1). The two must agree.
- **Consider:** The page uses the app's two real photographs plus a clearly-labeled format example for card anatomy (not a screenshot). That labeling is correct per §2.3/§5.8 — keep it labeled.

### 6.6 Mah Jongg Hand Finder landing (`apps/mah-jongg-hand-finder/index.html`)

- This is a landing page, not a Learn page in the §2 format. It is the Finder's Learn page in practice.
- **Must change:** No Apps dropdown in the top menu. Add it (all 5 apps, in home-page order).
- **Must change:** Eyebrow element exists but is empty. Fill it ("2026 Card · 79 Hands", matching the app) or remove the empty element.
- **Consider:** Bring its section structure into the §2.3 shape (first h2 "The app, at a glance", closing panel with App No. 1 pill) when it is next revised, rather than rebuilding it now.

### 6.7 Prime Factor Finder app (`apps/factor-finder/app.html`)

- **Must change (tokens):** Uses near-miss token values instead of the shared ones — ink `#1e2a21` (standard `#1e2b23`), line `#ded3ba` (standard `#ddd6c4`), green-strong `#175738` (standard `#17573a`), red-soft `#faeae6` (standard `#f7e3df`), gold-soft `#f6ecd0` (standard `#fbf0cd`), radius `16px` (standard `14px`), surface `#fffdf7` (no shared `--surface` token). Replace with the §1.1 tokens.
- **Must change (line-height):** Body line-height is `1.45`; prose in Help should be `1.6` (§1.2/§3.5).
- Otherwise conforms (brand-bar header, eyebrow, H1 = app name, numbered step h2s, Help last, footer one line).

### 6.8 CipherDesk app (`apps/cipherdesk/app.html`)

- **Must change (header):** Does not use the standard brand-bar markup (`brand-bar`/`brand-home`/`brand-logo`/`brand-sub`). It uses a lone `class="wordmark"` anchor and no `<header>` tag. Bring it into the standard header (§3.1) or record it as a deliberate exception. (The dark theme itself is a documented exception, §1.3 — the header markup is not.)
- **Must change (margins):** No `.wrap`; it uses `--page-max: 1080px` plus body padding. Use `.wrap` (§1.4/§3.5).
- **Must change (footer):** No `<footer>` element at all. Add the §3.4 footer (wordmark home link + one line + exponology.com).
- **Must change (Help position):** Last h2 is "Create a cryptogram", not "Help". Help must be the last h2 (§3.3).
- Dark-only palette is a documented exception (§1.3) — not a divergence.

### 6.9 Jigsaw Piece Finder app (`apps/jigsaw-piece-finder/app.html`)

- **Must change (lede):** The lede is 416 characters and explains how the app works (grid lines define pieces, matching four ways, board remembers, progress file). That duplicates the Learn page and the Help. Shorten it to one short paragraph (max ~200 characters) saying what the app does (§3.1/§5.2). The how-it-works detail already lives in the Learn page and the Help — link there, do not repeat it.
- **Must change (footer):** Footer says "Jigsaw Piece Finder is a work in progress at Exponology" and "scores are a first pass". The app is published with a Learn page — remove "work in progress" (§5.6). Keep the accuracy caveat, but move it to the Help (one place) phrased as what to check ("check SOFT and CONFLICT cards before placing"), not as a status label in the footer.
- **Must change (tokens):** Same near-miss token values as the Prime Factor Finder app (ink `#1e2a21`, line `#ded3ba`, green-strong `#175738`, red-soft `#faeae6`, gold-soft `#f6ecd0`, radius not set to `14px`). Replace with the §1.1 tokens.
- Otherwise conforms (standard brand-bar header — just standardized, eyebrow, H1 = app name, section h2s, Help last).

### 6.10 Mah Jongg Hand Finder app (`apps/mah-jongg-hand-finder/app.html`)

- **Must change (tokens):** Uses jade/red/gold accent values (documented exception, §1.3) but also near-miss base values — ink `#1c2b22`, line `#ddd2b8`, radius `16px`. Keep the jade accent; bring the base tokens (`--ink`, `--line`, `--radius`) into line with §1.1.
- **Must change (footer):** Footer is the full notation key (brackets, 0 = dragon, letters, NNNN). That text is repeated in the Learning Game app footer, the Matcher Learn page, and the Finder landing page (§5.1/§5.4). Move the full key to one home (the Finder landing "Key to the notation" section) and replace this footer with the §3.4 one-liner plus a link to the key.
- Otherwise conforms (brand-bar header, eyebrow, H1 = app name, section h2s, Help last).

### 6.11 The Mah Jongg Learning Game app (`apps/mah-jongg-hand-matcher/app.html`)

- **Must change (font):** Body font-family is `ui-sans-system, -apple-system, …` with no `"Public Sans"`. Add `"Public Sans"` as the first family (§1.2/§3.5).
- **Must change (background):** `--bg` is `#f6f1e6`, different from every other page's `#faf8f2`. Use the shared `--bg` (§1.1). (The jade accent is a documented exception; the page background is not.)
- **Must change (tokens):** Same near-miss base values as the Finder app (ink `#1c2b22`, line `#ddd2b8`, radius `16px`). Bring the base tokens into line with §1.1.
- **Must change (footer):** Footer is the full notation key plus the joker rule — the same duplication as §6.10. Move the full key to one home and replace this footer with the §3.4 one-liner plus a link to the key (and to the joker rule, which also lives in the Help).
- Otherwise conforms (brand-bar header, eyebrow, H1 = app name, section h2s, Help last).

### 6.12 Cross-page (the big ones)

- **Apps dropdown out of step.** Four different states exist today: home page (4 apps, no Jigsaw), CipherDesk Learn (4 apps, no Jigsaw), Jigsaw Learn (5 apps), PFF Learn and Matcher Learn (no dropdown at all). The standard (§2.1/§4) requires one dropdown with every live app, in home-page order, on the home page and every Learn page. Fixing this is a single coordinated change, not five separate ones.
- **App No. pills missing on two Learn pages.** PFF Learn (should be No. 4) and Matcher Learn (should be No. 2) have a closing section but no App No. pill. Add them (§2.3).
- **"(prototype)" and "work in progress" still on live pages.** PFF Learn footer, Matcher Learn footer, Jigsaw app footer. Remove on publish (§5.6).
- **The Mah Jongg notation key is in four places.** Hand Finder app footer, Learning Game app footer, Matcher Learn page, Finder landing page. Write it once, link to it (§5.1/§5.4).
- **Token drift.** The app pages use near-miss values (`#1e2a21` vs `#1e2b23`, `#ded3ba` vs `#ddd6c4`, `#175738` vs `#17573a`, radius `16px` vs `14px`) instead of the shared tokens. Replace with the §1.1 tokens so a future color change is one edit, not five.

---

## 7. How to use this standard for a new app

1. Copy the shared tokens (§1.1), fonts (§1.2), and `.wrap` (§1.4) verbatim. Do not adjust them.
2. Build the Learn page to §2 (top menu with Apps dropdown + Open button, eyebrow + H1 + short lede, "The app, at a glance" first, one section per step, closing panel with the App No. pill, footer without "(prototype)").
3. Build the app page to §3 (standard brand-bar header, same eyebrow, H1 = app name, short lede, section h2s, Help last, one-line footer).
4. Add the app to the home page (card + Apps dropdown) and to every Learn page's Apps dropdown, in the same step. The App No. on the new Learn page must match the new home-page card number.
5. Write each fact once (§5). If you catch yourself pasting an explanation from the Learn page into the app (or vice versa), link instead.
6. Verify against §6's checklist before publishing: Apps dropdown present and complete, App No. pill present and correct, eyebrow present and non-empty, no "(prototype)"/"work in progress", footer one line, Help last on the app, no near-miss token values.
