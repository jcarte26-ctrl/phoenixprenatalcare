[README (1).md](https://github.com/user-attachments/files/29299977/README.1.md)
# Access to Prenatal Care in the Phoenix Metropolitan Area

A bilingual (English / Spanish) web directory that helps expecting families across the Phoenix metro area find pregnancy clinics, safe shelter, and support services. Built as a single, self-contained HTML file — no build tools, no API keys, no server. Brought to you by **Dr. Lexi**.

🔗 **Live site:** _add your GitHub Pages URL here_

---

## Contents

- [What's inside](#whats-inside)
- [Quick start](#quick-start)
- [Deploying to GitHub Pages](#deploying-to-github-pages)
- [How it's built](#how-its-built)
- [Updating the content](#updating-the-content)
  - [Add or edit a clinic](#add-or-edit-a-clinic)
  - [Add or edit a shelter](#add-or-edit-a-shelter)
  - [Edit the Resources tab](#edit-the-resources-tab)
  - [Translations](#translations)
  - [Replacing the logo](#replacing-the-logo)
- [Design notes](#design-notes)
- [Data sources & safety choices](#data-sources--safety-choices)
- [Disclaimer](#disclaimer)

---

## What's inside

Three tabs, each fully translated:

1. **Pregnancy Clinics** — 33 OB-GYN practices, perinatal specialists, and sliding-scale community health centers, grouped by ten areas (Central, North, South, West Phoenix, Glendale, Scottsdale, Tempe, Mesa, Chandler, Gilbert). Filter by area; an interactive map below updates to match, and every card links to Google Maps and a tap-to-call number.
2. **Women's Shelters** — Emergency domestic-violence programs, family shelters, and transitional housing, grouped by region. Domestic-violence shelters are listed by **phone intake only** (their addresses are confidential by design). Family/transitional shelters with public addresses are shown on the map.
3. **Resources & Support** — A 24/7 crisis strip, a tappable "What do you need right now?" chooser, six resource cards (paying for care, WIC/food, know-your-rights, immigrant families, mental health, free supplies), and an expandable trimester-by-trimester roadmap.

Everything runs client-side. A visitor only needs a browser.

---

## Quick start

```bash
# Just open the file — that's it.
open prenatal-phoenix.html        # macOS
xdg-open prenatal-phoenix.html    # Linux
start prenatal-phoenix.html       # Windows
```

The maps (Leaflet + OpenStreetMap) and fonts (Google Fonts) load from public CDNs, so the page needs an internet connection to show map tiles and the custom typefaces. All the clinic/shelter data and the logo are baked into the file itself.

---

## Deploying to GitHub Pages

The whole site is one file, so deployment is simple.

1. Put `prenatal-phoenix.html` in your repository. To serve it at the site root, rename it:
   ```bash
   mv prenatal-phoenix.html index.html
   git add index.html
   git commit -m "Publish prenatal care directory"
   git push
   ```
2. In your repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, pick your branch (e.g. `main`) and the `/ (root)` folder, then **Save**.
4. Wait a minute, then visit `https://<your-username>.github.io/<your-repo>/`.

> **Tip:** If you keep the filename as `prenatal-phoenix.html` instead of `index.html`, your URL becomes `https://<your-username>.github.io/<your-repo>/prenatal-phoenix.html`.

---

## How it's built

| Piece | What it uses |
|---|---|
| Markup & styling | Hand-written HTML + CSS (no framework) |
| Interactivity | Vanilla JavaScript (no dependencies to install) |
| Maps | [Leaflet 1.9.4](https://leafletjs.com/) via cdnjs, with free [OpenStreetMap](https://www.openstreetmap.org/) tiles |
| Fonts | Google Fonts — **Fraunces** (display) + **DM Sans** (body) |
| Logo | The Dr. Lexi PNG is embedded directly in the HTML as a base64 data URI, so it can never break on deploy |
| Map links | Google Maps links are generated automatically from each place's name + address |

All content lives in plain JavaScript arrays near the bottom of the file, inside the final `<script>` block. You don't need to touch the HTML or CSS to update listings.

---

## Updating the content

Open `prenatal-phoenix.html` in any text editor and scroll to the `DATA` section in the last `<script>` block. Each listing is a simple array (a "row"). Keep the field order exactly as shown.

### Add or edit a clinic

Clinics live in the `CLINICS` array. Row format:

```js
// [ name, areaId, address, latitude, longitude, phone, flag ]
["Lilac Ob-Gyn", "chandler", "655 S Dobson Rd Ste 101, Chandler, AZ 85224",
 33.2946811, -111.8756382, "4804592555", null],
```

- **name** — display name. Write an ampersand as `&amp;`.
- **areaId** — must match an id in `CLINIC_HOODS` (`central`, `north`, `south`, `west`, `glendale`, `scottsdale`, `tempe`, `mesa`, `chandler`, `gilbert`).
- **address** — full street address; used for the map pin and the Google Maps link.
- **latitude / longitude** — decimal coordinates. The quickest way to get these: right-click the spot in Google Maps → the numbers at the top are `lat, lng`.
- **phone** — digits only, no `+1` and no punctuation (e.g. `"4804592555"`). The site formats it for display.
- **flag** — use `"fqhc"` to show a "Sliding scale" badge, otherwise `null`.

To add a new **area**, add a row to `CLINIC_HOODS` in the form `["id","English label","Spanish label"]`, then use that `id` on your clinic rows.

### Add or edit a shelter

Shelters live in the `SHELTERS` array. Row format:

```js
// [ name, regionId, type, address|null, lat|null, lng|null, phone|null, desc_en, desc_es ]
["Sojourner Center", "cphx", "dv", null, null, null, "6022440089",
 "One of the nation's largest domestic-violence shelters. Pet friendly, on-site childcare, Spanish-language services.",
 "Uno de los refugios de violencia doméstica más grandes del país. Admite mascotas, cuidado infantil y servicios en español."],
```

- **regionId** — must match an id in `SHELTER_REGIONS` (`cphx`, `nphx`, `west`, `mesa`, `chgi`).
- **type** — controls the badge and whether it appears on the map:
  - `"dv"` → domestic-violence program. **Leave address/lat/lng as `null`** so it is *not* mapped, and it shows a "Confidential — call first" badge.
  - `"family"` → family/transitional shelter. Provide an address + coordinates to place it on the map (coral pin).
  - `"preg"` → housing specifically for pregnant women. Provide address + coordinates (gold pin) and a "For pregnant women" badge.
- **desc_en / desc_es** — one-sentence description in each language.

> **Please keep domestic-violence shelter addresses out of the file.** Listing them by phone intake only is a deliberate safety choice (see [below](#data-sources--safety-choices)).

### Edit the Resources tab

- **Resource cards** — the `RESOURCES` array. Each card has a `title`, a `body`, and a list of `rows`. Every text field uses the `R("English","Spanish")` helper. A row is `[ R(label), R(value), href ]`; set `href` to a `tel:` number, a `https://` URL, or `null` for plain text.
- **"What do you need" buttons** — the `NEEDS` array. Each entry points at a resource card `id` so the button scrolls to and highlights it.
- **Trimester roadmap** — the `ROADMAP` array. Each stage is `[ color, R(title), R(htmlBulletList) ]`.

### Translations

All interface text lives in the `I18N` object (`I18N.en` and `I18N.es`). Listing descriptions carry their own English/Spanish fields as described above. To change wording, edit the matching key in both `en` and `es`. The language toggle is in the top-right corner; English is the default.

### Replacing the logo

The Dr. Lexi logo is embedded as a base64 data URI on the `<img class="bb-logo" ...>` tag inside the hero. To swap it:

1. Convert your new PNG to base64 (for example, `base64 -w0 logo.png` on Linux, or any online encoder).
2. Replace everything after `src="data:image/png;base64,` (up to the closing quote) with the new string.

A transparent-background PNG looks best, since the logo sits inside a light pill.

---

## Design notes

The look is a Sonoran-desert-at-dusk palette — indigo sky fading into sunset coral and desert gold — with a hand-drawn saguaro horizon as the signature motif (it reappears as the map pins). Turquoise is the interactive accent. The build aims for a quality floor: responsive down to mobile, visible keyboard focus, and reduced-motion support (the animated sun glow is disabled for visitors who prefer reduced motion).

---

## Data sources & safety choices

- Listings were compiled from **public business and organization records** in **June 2026**. Names, addresses, and coordinates were taken from public mapping data; the crisis hotline numbers were verified against state and county sources.
- **Domestic-violence shelters are listed by phone intake only.** Their physical locations are kept confidential to protect residents, so the site never maps them. The Maricopa County shelter screening line (480-890-3039) is shown prominently as the right starting point.
- The directory favors verified entries over completeness. A few listings were thinner in the public record and are worth re-confirming before heavy promotion.
- Because details change, **the site tells visitors to call ahead** and treats every entry as something to confirm, not a guarantee.

---

## Disclaimer

This site provides **information, not medical or legal advice**. In a medical emergency, call **911** — an emergency room cannot turn someone away during active labor, regardless of ability to pay or immigration status. Verify hours, accepted insurance, intake availability, and addresses directly with each organization before relying on them.

---

_Brought to you by Dr. Lexi._
