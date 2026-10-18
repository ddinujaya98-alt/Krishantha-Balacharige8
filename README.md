# Personal Portfolio Website

A premium, responsive **six-page** portfolio for **Krishantha Balacharige** — a
**jewellery designer and craftsman** in Sri Lanka (bespoke commissions, rings and
bridal sets, stone setting, resizing and repairs) — built around the **official KB
logo** with a dark-luxury **burnt-orange & black** cinematic design. Plain HTML, CSS
and JavaScript. No frameworks, no build step, no dependencies.

## Pages

| File             | Page     | Contents                                                      |
| ---------------- | -------- | ------------------------------------------------------------- |
| `index.html`     | Home     | Hero with animated portrait, marquee, about preview, what I make, the craftsman, featured projects |
| `about.html`     | About    | Introduction, philosophy, strengths, highlights               |
| `projects.html`  | Projects | Filterable jewellery gallery (bespoke / bridal / stone / repairs) + commission process |
| `project.html`   | Project  | One project in detail: specs, story, photo gallery + lightbox, related projects |
| `experience.html`| Experience | Editable timeline: bench work, commissions, training, milestones |
| `contact.html`   | Contact  | Contact info, socials, validated form with `mailto:` handoff  |

## How to view

Double-click **`index.html`** — it opens directly in your browser. No installation,
no server required.

> Fonts load from Google Fonts when you're online. Offline, the site falls back to
> system fonts and still works.

## Folder structure

```
├── index.html
├── about.html
├── projects.html
├── project.html        ← one project in detail (project.html?id=…)
├── experience.html
├── contact.html
├── css/
│   └── style.css       ← all styles + colour tokens
├── js/
│   ├── projects-data.js ← the shared project list (samples + your saved edits)
│   ├── project-page.js  ← renders one project + its photo gallery/lightbox
│   ├── admin.js         ← hidden admin panel (loads before main.js)
│   └── main.js          ← menu, reveal, filters, form
├── assets/
│   ├── kb-logo.png       ← YOUR ORIGINAL LOGO (untouched, full-res, pure white)
│   ├── kb-logo-monogram-clean.png ← YOUR GLOSSY ORANGE MONOGRAM (small marks)
│   ├── favicon.png       ← browser-tab icon (mark on a dark tile)
│   ├── portrait.png      ← YOUR PORTRAIT (transparent PNG)
│   └── portrait-about.png ← about-page portrait (transparent PNG)
└── README.md
```

> On every page the scripts must load in this order:
> **`projects-data.js` → `admin.js` → `main.js`** (`project.html` also loads
> `project-page.js` before `main.js`). `projects-data.js` draws the project grid,
> `admin.js` overlays your saved edits, and `main.js` then wires up the filters and
> scroll reveals.

## What to edit

### The content theme

All copy across the five pages is written around **handcrafted jewellery**: bespoke
commissions, rings and bridal sets, stone setting, and resizing/repairs. The place to
change it:

- **Titles & meta descriptions** — the `<title>` and `<meta name="description">` of each page.
- **Hero, marquee, services, stats, CTA** — `index.html`.
- **Philosophy, strengths, working principles** — `about.html`.
- **The eight projects + filter bar** — `projects.html` (`data-category` / `data-filter`).
- **One project's page** — `project.html` (the shell; the words come from `js/projects-data.js`).
- **Project words & samples** — `js/projects-data.js` (`DEFAULTS`: title, category, description, story, metal, stones, finish, timeframe, tags, artwork colours, photographs).
- **Timeline, skills, CTA** — `experience.html`.
- **Info cards, socials and the form's service list** — `contact.html`.
- **Categories and colour presets** — `CATS` and `PRESETS` in `js/admin.js`.

Everything above is plain English text inside the HTML/JS, so it can be edited without
touching the CSS. The four categories (`bespoke`, `bridal`, `stone`, `repair`) must match
in `projects.html` and in `CATS` in `js/admin.js`.

### Your name and logo
The site is branded **Krishantha Balacharige**. To change the name, find & replace
`Krishantha Balacharige` across the HTML files, and update the footer credit line
(which the admin panel also controls via your **account name**). Keep each `<title>`
and `meta description` in sync too.

The brand mark is **your real KB logo image**, not text. Its silhouette and transparency
come straight from your original file — nothing is ever redrawn, rotated or stretched.
It appears in three places:

| Where | Markup |
| --- | --- |
| Header + footer brand link | `<img class="brand-mark" src="assets/kb-logo-monogram-clean.png" …>` |
| Admin panel (sign-in + signed-in line) | `<img class="adm-brand-mark" src="assets/kb-logo-monogram-clean.png" …>` |

> The **home-page hero shows your portrait**, not the logo (see below). The KB mark
> still appears in the header, footer, favicon and admin panel on every page.

The logo files live in `assets/`:

- **`assets/kb-logo-monogram-clean.png`** — your glossy orange monogram, **cropped tight to the artwork** (506 × 512, aspect preserved). The source image had ~53% transparent margin around the symbol, which made the mark look small; the padding is trimmed so the symbol fills its box. Used for the header, footer and admin marks.
- **`assets/kb-logo.png`** — your original upload, **byte-for-byte untouched** (2326 × 2537, transparent, pure white).
- **`assets/kb-logo-brand.png`** — the mark filled with the site's own gradient (light peach → `--accent-2` → `--accent` → deep ember) plus a white gloss highlight. 760 × 829. Kept, not referenced.
- **`assets/kb-logo-glossy-monogram.png`** — an earlier full-frame variant of the monogram (1024 × 1536). Kept, not referenced.
- **`assets/kb-logo-mark.png`** — the older gradient small mark. Kept, not referenced.
- **`assets/favicon.png`** — 180 × 180 browser-tab icon: the gradient mark on a `#130b0b` rounded tile.

The marks are plain `<img>` elements: the height is a fluid `clamp()` and `aspect-ratio`
matches the file, so they scale with the viewport and never stretch or rotate. Because the
monogram art is cropped to its edge, the visible symbol fills the box instead of floating in
transparent padding.

**Want the plain white mark instead?** Point the `<img>` tags above at
`assets/kb-logo.png` and it will render in pure white exactly as uploaded.

To swap the logo later, replace `assets/kb-logo.png` with a new transparent PNG and
regenerate the smaller versions (the CSS only sizes the mark — it never rotates,
stretches or crops it).

### The stacked hero name
The home-page name is set as two editorial lines, purely by the CSS rule
`.hero-name .accent-word` (the `<h1>` text itself is unchanged):

```html
<h1 class="hero-name hero-anim hero-anim-2">Krishantha <em class="accent-word">Balacharige.</em></h1>
```

- **`Krishantha`** — line one, the heavy sans (weight 800).
- **`Balacharige.`** — line two, italic display serif (Fraunces) at `1em` (the same size as
  line one) in a flat `--accent-2` colour.

`display: block; width: fit-content` on the accent word breaks the line while keeping the
text box hugging the text. Tune the second line in `css/style.css` via its `font-size`
(`1em`), `line-height` (`1.1`) and `margin-top` (`0.1em`).

The old `<h2 class="hero-headline">Creative Designer &amp; Digital Experience Creator</h2>`
line was removed from `index.html` at the owner's request; its `.hero-headline` CSS block is
still in `css/style.css` so the line can be dropped back in whenever it is wanted.

> **Never put `background-clip: text` on these accent `<em>` elements.** The hero reveal
> wraps every word in an `overflow: hidden` mask (`js/main.js` → `splitWords`), and
> Chromium then paints nothing at all: the text stays transparent and no gradient is
> drawn, so the accent words silently disappear from the page. They are a flat colour for
> exactly this reason.

### Your portrait
Your portrait is the **hero visual on the home page**, and a second shot appears on
`about.html`. There are two files:

- **`assets/portrait.png`** — the home hero. Currently **1882 × 3340 px** (ratio ≈ 0.564).
- **`assets/portrait-about.png`** — the `about.html` portrait. Currently **1089 × 1445 px** (ratio ≈ 0.754).

Replace either with your own photo — ideally a **transparent PNG** (cut-out).

If your photo has a different aspect ratio, update `aspect-ratio` in these rules in
`css/style.css`:

- `.portrait-stage__figure` — the home hero (plus its `height` clamp, so it scales with the screen)
- `.split-portrait img` — the `about.html` portrait

The site blends the cut-out into the dark background with warm ambient lighting, so
transparent edges look best. If your photo has a solid background it still works — it
will simply show as a photo.

The hero portrait deliberately has **nothing layered behind it** — no halo, no rotating
ring, no light sweeping across the photo. The owner removed those. What is left:

- a soft rise-and-focus reveal on load (`@keyframes portrait-reveal`),
- a slow float with a hint of breathing (`@keyframes portrait-float`),
- a static contact shadow underneath (`.portrait-stage__base`),
- a **3D tilt that follows the pointer** — the portrait turns slightly towards the
  cursor (`js/main.js`, section 8; the transform on `.portrait-stage__img`).

> The tilt writes a plain `transform` string from JavaScript. A `var()`-driven
> transform does **not** animate through the CSS `transition` in Chromium — the element
> just stays at its old value — so keep the values out of custom properties.

### Colours
All colours live at the top of `css/style.css` in the `:root` block:

```css
--bg: #130b0b;        /* main background */
--bg-2: #1c1110;      /* secondary background / cards */
--bg-3: #241614;      /* raised panels */
--accent: #ff681e;    /* burnt orange (used sparingly) */
--accent-2: #ff8b46;  /* lighter orange */
--text: #fff8f0;      /* main text */
--text-2: #b6a49a;    /* secondary text */
--logo: #ffffff;      /* pure-white mark (if you switch the logo back) */
--burgundy: #2b1417;  /* hero logo-plate surface */
--burgundy-2: #3a1d20;/* hero logo-plate highlight */
--logo-1: #ffc79a;    /* KB mark gradient — light peach highlight */
--logo-2: #ff8b46;    /* KB mark gradient — warm orange */
--logo-3: #ff681e;    /* KB mark gradient — brand orange */
--logo-4: #ce3007;    /* KB mark gradient — deep ember */
```

Change a value and save — it updates everywhere instantly. Remember to bump the
`?v=` number on the `css/style.css?v=` link in each page so browsers pick it up.

### Email address
Two places on **`contact.html`**:
1. The `data-email` attribute on the `<form>` element.
2. The visible `mailto:` links (also in the footer of every page).

### Social links
Search for `EDIT: replace with your real profile URLs` — links appear in the footer of
every page and on the contact page.

### Projects

Each project is one `<article class="project-card">` in `projects.html` — it is the
**no-JavaScript fallback**. With JavaScript on, `js/projects-data.js` takes over: it
draws the same eight projects, swaps in any project you edited in the admin panel, and
injects the ones you add there. The card markup is:

- `data-project="aurelia"` — the project's id. This is what ties the card to its detail
  page and to any edits you save in the admin panel, so **keep it unique**.
- `data-category="bespoke"` decides which filter shows it — the four categories are
  `bespoke`, `bridal`, `stone` and `repair` (space-separated for several, e.g.
  `data-category="bridal stone"`). The filter buttons in `.filter-bar` use the same
  words in their `data-filter`.
- `data-sample="1"` marks the eight built-in samples so the admin's “Hide the sample
  projects” option can remove them.
- The `↗` is a real link to `project.html?id=<the id>`; the CSS stretches it over the
  whole card, so clicking anywhere on a card opens that project.

Every card you add or edit **in the admin panel** is written to
`js/projects-data.js`'s list and instantly gets its own detail page too.

### A project's own page

`project.html` reads the `?id=` from the address bar and renders that one project:
the big visual, the **Metal / Stones / Finish / Timeframe** rows, tags, the full story,
and an **“Other projects”** row at the bottom. With no photos it draws the generated
artwork and the line “Photographs of this piece are coming soon.”; with photos it shows
a gallery — click the big image to open the **lightbox** (←/→ to move, Esc to close).

An unknown id shows a friendly “that project could not be found” card instead of a
blank page.

### Adding real photographs to a project

Photographs are **files, not uploads**: drop the image into `assets/`
(e.g. `assets/aurelia-1.jpg`), then list its path in the admin panel under
**Projects → (edit) → Photographs**, **one per line**:

```
assets/aurelia-1.jpg
assets/aurelia-2.jpg
assets/aurelia-detail.jpg
```

The first line becomes the main image, the rest become thumbnails. Keep the files
small (roughly 1200–1600 px on the long edge, JPEG) so the page stays fast.

> Photos are referenced by path, not embedded into the browser's storage — so keep the
> files in `assets/` (or any folder you like under the site) and use paths relative to
> the site root. Each path is shown exactly as typed.

### Experience entries
Open `experience.html` and replace every `[bracketed placeholder]` with your real
roles, dates, organisations and achievements. The current entries are **templates,
not a real work history**.

## Hidden admin panel

The site has a password-protected admin panel built into every page — **no backend,
no external tools**. You open it from the footer.

### Opening it

**Triple-click the footer line that says “Powered By Krishantha Balacharige”**
(or focus it with Tab and press Enter). The panel slides up.

### The security key

There is **no setup screen**. The panel ships with a **built-in short key** that is
**never shown on screen** — not in the panel and not as plain text anywhere in the
page. It is stored only as an unreadable hash (`js/admin.js` contains the hash, never
the key itself). Type it on the login screen and click **Unlock panel** (or press
Enter). You can change it any time under **Settings → Security key**.

### What you can do

| Tab | What it does |
| --- | --- |
| **Overview** | Page views with **dates**, views per page, recent activity, last-viewed time, project count |
| **Projects** | **Add / edit / hide / delete projects** — full details, photographs, colours and tags; saved projects appear in the grid and on their own detail page |
| **Messages** | Every message sent through the contact form **on this browser**, with a count badge on the tab |
| **Settings** | Change your **account name**, change the security key, export/import a backup, log out |

**Account name** — shown as “Powered By …” in the footer of every page.

**Adding a project** — give it a title, category label, one or more categories
(**Bespoke / Rings & Bridal / Stone Setting / Repairs**), a short description, the full
story, the **Metal / Stones / Finish / Timeframe** rows, **photographs** (one path per
line — see above), an artwork style (colour presets or custom colours), tags and an
optional link. The artwork letter defaults to the first letter of the title. Saving
takes you straight to a refreshed view so you can see the result.

**Editing a sample** — the eight built-in projects can be edited like any other. They
keep their id, so your version replaces the sample everywhere (grid **and** detail
page). A “Reset to sample” button appears while editing one, and the list shows
“edited sample” next to it.

**Hide vs delete** — the built-in samples are **hidden**, not deleted: use the
**Hide** button on their row, then **Restore** to bring them back. Projects *you* added
are really deleted. The “Hide the sample projects” tick still removes all the untouched
samples in one go, which is the cleanest option once you have added your own work.

**Messages** — the contact form keeps a copy of each message here (newest first, with
the visitor's name, email, chosen service, the message and the time), and the tab shows
how many are waiting. You can delete one or clear the whole list. **Honest limit:** this
site has no backend, so a message is only saved in the browser it was sent from — a
visitor's message on their own device cannot appear in this list. The visitor's email
app still opens with the message addressed to you, which is how you actually receive it.
To collect messages from everyone, point the form at a form service (like Formspree) or
a small backend.

**Backup** — everything is stored in **this browser only** (localStorage). Before
clearing cookies or moving to another device, use **Settings → Export backup**, then
**Import backup** on the new device or browser. The backup includes your projects,
hidden samples, account name and the messages inbox.

**Backup** — everything is stored in **this browser only** (localStorage). Before
clearing cookies or moving to another device, use **Settings → Export backup**, then
**Import backup** on the new device or browser.

### Changing the security key

Settings → Security key → enter your current key, then type the new key you want
(**short keys only — up to 20 characters**), and click **Update key**. The new key is
stored as a hash and is **never shown on screen**.

### If you forget the key

On the login screen, click **Reset access**. This clears the key *and* your saved
projects, messages and stats on that browser, then **restores the built-in key** so you
can log straight back in.

> **Honest note on security:** this is a client-side gate, not real server security.
> It keeps casual visitors out and hides the panel, but anyone with access to the
> browser's developer tools could read or reset what is stored locally. Do **not**
> put sensitive information in it.

## The contact form (important)

This site is static — **there is no backend**. The form validates input, then opens
the visitor's own email app with the message pre-filled and addressed to you
(via `mailto:`). Nothing is sent to a server, and the page says so honestly.

The form also keeps a **local copy** of each message in the admin panel's
**Messages** tab — but only *in the browser the message was sent from*, so you will
only ever see messages sent from your own device. Treat it as a convenience log; the
email is still the real delivery.

If you later want real server-side sending, point the `<form>` at a form service such
as Formspree, Netlify Forms or your own endpoint — the fields (`name`, `email`,
`service`, `message`) are already named and ready. As soon as a form service starts
handling submissions, remove the `mailto:` line in `js/main.js` (section 6) if you want
to stop it spawning the visitor's email app.

## Home page animations (how to tune or remove)

The home page (`index.html`) has an extra cinematic motion layer. Everything is
scoped to `body.home`, so the other five pages are untouched. It lives in
`css/style.css` under the comment **"18b. Home — cinematic motion layer"** and in
`js/main.js` under **"9. Home page — cinematic motion layer"**.

| Effect | Where to tune |
| --- | --- |
| Drifting background orbs | `.hero-orb-1/2/3` and `@keyframes orb-drift-*` (size, colour, speed) |
| Word-by-word headline reveal | `.home .wi` → `animation-delay` and `.home .hero-name { --word-base }` |
| Hero portrait reveal (rise + un-blur) | `.portrait-stage__figure` → `@keyframes portrait-reveal` |
| Hero portrait float + slow breathing | `.portrait-stage__figure` → `@keyframes portrait-float` |
| Portrait turning with the pointer (3D tilt) | `.portrait-stage__img` (`transform` + `transition`) and `main.js` (8) |
| Portrait section fade/rise (about) | `.split-portrait[data-reveal]` + ambient glow via `.split-portrait::before` |
| Top scroll-progress line | `.home .scroll-progress` |
| Magnetic buttons | `.home .btn` (`--mag-x/--mag-y`) + `strength` in `main.js` (9c) |
| Pointer spotlight on cards | `.home .card::after` (…) + `main.js` (9d) |
| Hero pointer glow | `.hero-cursor-glow` + `main.js` (9e) |
| Section "focus-in" reveal | `.js .home [data-reveal]` (blur/translate) |

To **turn the whole layer off**, just remove `class="home"` from the `<body>` tag of
`index.html` — every rule and script is gated on it. To keep the look but drop the
motion, leave `home` in place; the OS "reduced motion" setting already disables it.

## Accessibility & motion

- Semantic HTML5, skip links, labelled inputs, `aria-current` on active nav.
- Keyboard-visible focus rings, hamburger menu closes with Escape.
- All animations respect the OS **"prefers reduced motion"** setting; the
  headline word-split is skipped entirely and the decorative layers are hidden.

## Browser support

Modern evergreen browsers (Chrome, Edge, Firefox, Safari). Uses `svh` units, CSS
grid, custom properties and `IntersectionObserver`.
