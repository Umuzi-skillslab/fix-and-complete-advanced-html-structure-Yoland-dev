# Media Production Company — Website

## Overview
A four-page static website for a fictional media production company offering video production, audio recording, and photography services. Pages: **Home** (`index.html`), **About** (`about.html`), **Media** (`media.html`), and **Contact** (`contact.html`). All pages share a single stylesheet (`css/styles.css`).

---

## Issues Found in Starter Code

- `font-family: Arial` — generic, no fallback stack
- Only **2 selector types** used (element + class); requirement was 5+
- Only **1 pseudo-class** used (`:hover`); requirement was 5+
- **No flexbox layouts** on hero or footer sections
- **No CSS Grid** anywhere in the stylesheet
- **No keyframe animations**, transforms, or transitions
- **No text effects** (shadows, gradients)
- **No media queries** — site was not responsive
- Form fields had `display: block` with minimal padding — all inputs rendered on a single line with no layout
- `<video>` second element had typo `type="vido/mp4"`
- Portfolio images used fixed pixel `height` with no `object-fit`, causing distortion
- `<figure>` and `<figcaption>` were not defined
- No `:focus` styles — keyboard navigation had no visible indicator

---

## Fixes and Implementations

### Flexbox Layouts (4 implemented)
1. **`.top` header** — `justify-content: space-between` aligns the logo left and nav right, with `flex-wrap` for small screens
2. **`.nav`** — horizontal link row with consistent `gap`, collapses cleanly on mobile
3. **`.hero`** — `flex-direction: column` centres content vertically within the full-height section
4. **`.bottom` footer** — centres contact items horizontally, stacks vertically at 768px

### CSS Grid Layouts (3 implemented)
1. **`.content`** (homepage) — `1fr 2fr` two-column split separating the heading from the body text
2. **`.services-container`** (about) — `repeat(3, 1fr)` equal card columns, collapses to 1 column on tablet
3. **`fieldset`** (contact form) — `1fr 1fr` pairs fields naturally; full-width fields use `grid-column: 1 / -1`

### Selector Types Added (6 total)
| # | Type | Example |
|---|------|---------|
| 1 | Element | `body`, `h1`, `figure`, `audio` |
| 2 | Class | `.hero`, `.service-card`, `.portfolio-grid` |
| 3 | Descendant | `.nav a`, `.service-card h3`, `figure img` |
| 4 | Attribute | `input[type="email"]`, `video[controls]`, `iframe[src*="google.com/maps"]` |
| 5 | Pseudo-class | `:hover`, `:focus`, `:valid`, `:first-child`, `:last-child`, `:nth-child()`, `:active`, `:checked`, `:last-of-type` |
| 6 | Pseudo-element | `::before`, `::after`, `::placeholder` |

### Animations, Effects, Transforms & Transitions
- **`@keyframes fadeUp`** — hero text and about section paragraphs fade and rise on load
- **`@keyframes slideInLeft`** — site title slides in from the left on every page
- **`@keyframes underlineExpand`** — nav link underline scales from 0 to full width on hover
- **Text shadow** — `text-shadow` on `h1` for depth against the dark header
- **Gradient text** — `background-clip: text` on `.hero h2` fades white into the brand orange
- **Transforms** — `translateY(-5px)` lifts cards and buttons on hover; `scaleX(1)` expands nav underlines; `scale(1.03)` zooms portfolio images
- **Transitions** — applied to border-color, box-shadow, transform, color, and background-color throughout, all using a consistent `0.25s ease` variable

### Accessibility Improvements
- `:focus` styles added to all nav links, inputs, and the submit button using a visible `outline` in the accent colour
- `accent-color` applied to radio, checkbox, and audio player controls
- Colour contrast fixed on `.hero` — white text on dark background (passes WCAG AA)
- `aria-current="page"` attribute selector used to style the active nav link semantically
- All images include `alt` attributes; `object-fit: cover` prevents distortion
- `placeholder` colour kept at sufficient contrast (`#bbb` on white)

### Cross-Browser Compatibility
- `clamp()` used for fluid font sizes — supported in all modern browsers (Chrome 79+, Firefox 75+, Safari 13.1+)
- `-webkit-background-clip: text` included alongside the standard `background-clip: text` for Safari
- `appearance: none` on `<select>` with a custom SVG chevron ensures consistent rendering across Chrome, Firefox, and Safari
- `accent-color` is supported in Chrome 93+, Firefox 92+, Safari 15.4+; older browsers fall back to default control styles gracefully
- `position: sticky` on `.top` requires no prefix in modern browsers; disabled (falls back to `static`) on mobile via media query to avoid iOS scroll bugs

---

## Viewing Locally

1. Clone or download the project folder
2. Ensure the folder structure is:
   ```
   project/
   ├── css/styles.css
   ├── images/
   ├── media/
   ├── index.html
   ├── about.html
   ├── media.html
   └── contact.html
   ```
3. Open `index.html` in any modern browser — no server required

---

## Known Issues / Limitations

- `label:has(...)` is used for radio/checkbox layout — not supported in Firefox below version 121
- The Google Maps `<iframe>` requires an active internet connection to render
- Form has no backend — `<form>` submission reloads the page; a server or service (e.g. Formspree) would be needed for real submissions
- The `video[controls]` typo (`type="vido/mp4"`) in the original HTML should be corrected manually in `media.html`
