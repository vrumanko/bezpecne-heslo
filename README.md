# Bezpečné Heslo — Secure Password Generator

A single-file, client-side password generator with a clean Slovak UI. No build tools, no frameworks, no server — open `index.html` and use it.

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)

---

## Features

- **Cryptographically secure** — uses `crypto.getRandomValues()` with rejection sampling to eliminate modulo bias; no `Math.random()`.
- **Fisher-Yates shuffle** — character classes are distributed uniformly, never grouped by type.
- **Entropy + crack-time estimate** — displays bit entropy and estimated offline brute-force time (10¹⁰ guesses/sec assumption, conservative GPU cluster baseline).
- **5-level strength indicator** — segmented bar with color coding (Very Weak → Very Strong).
- **Configurable composition** — sliders for total length (4–64), digit count, and special character count; constraints enforced so digits + special ≤ length.
- **Exclude similar characters** — optionally removes visually ambiguous glyphs (`I`, `l`, `1`, `O`, `0`). Entropy calculation reflects the reduced pool.
- **Persistent settings** — slider positions and toggle state survive page reloads via `localStorage` (`bezpecneHeslo:settings:v1`). Passwords are **never** persisted.
- **Stale-state UX** — changing any control greys out the current password and disables Copy until a new password is generated.
- **Keyboard shortcut** — `Enter` generates a new password from anywhere on the page (skips when a button is focused to avoid double-fire).
- **Click to select** — clicking the password field selects the full text for instant manual copy.
- **Clipboard API with fallback** — uses `navigator.clipboard` in secure contexts; falls back to `execCommand('copy')` for older browsers and non-HTTPS environments.
- **Accessible** — `aria-live`, `role="progressbar"`, `aria-label`, `focus-visible` outlines, `aria-hidden` on decorative SVGs.
- **Responsive** — single-column layout on narrow screens; 2-column stats grid on mobile.
- **Reduced motion** — all animations and transitions are suppressed when `prefers-reduced-motion: reduce` is set.

---

## Usage

```bash
# Clone or download
git clone https://github.com/<your-username>/bezpecne-heslo.git

# Open directly — no server required
open index.html
```

For clipboard access in Chrome/Edge without a local server, serve over HTTP:

```bash
npx serve .
# or
python3 -m http.server 8080
```

---

## How It Works

### Entropy calculation

```
entropy = length × log₂(charsetSize)
```

`charsetSize` is the union of active pools after optional similar-character filtering:

| Pool | Full size | Filtered (exclude similar) |
|---|---|---|
| Letters (a–z + A–Z) | 52 | 44 |
| Digits (0–9) | 10 | 8 |
| Special (`!@#…`) | 26 | 26 (unchanged) |

### Strength thresholds

| Score | Label | Entropy |
|---|---|---|
| 1 | Veľmi slabé | < 28 bits |
| 2 | Slabé | 28–39 bits |
| 3 | Primerané | 40–59 bits |
| 4 | Silné | 60–79 bits |
| 5 | Veľmi silné | ≥ 80 bits |

### Crack-time estimate

```
seconds = 2^entropy / 2 / 10^10
```

Models an offline fast-hash attack (e.g. unsalted MD5/NTLM on a GPU cluster). The "÷ 2" accounts for the attacker finding the password on average halfway through the search space.

---

## Security Notes

- All randomness comes from `crypto.getRandomValues()` (CSPRNG). The rejection-sampling loop ensures a perfectly uniform distribution with no modulo bias.
- Passwords are generated and displayed in-browser only. Nothing is transmitted or stored.
- `localStorage` stores settings (length, digits, special, excludeSimilar) only — never password values.
- The entropy formula assumes a purely random password. Real-world threat models differ; treat the crack-time as an order-of-magnitude guide, not an exact figure.

---

## Browser Support

Any modern browser with `crypto.getRandomValues()` support — Chrome 11+, Firefox 21+, Safari 6.1+, Edge 12+. The `execCommand('copy')` fallback covers non-HTTPS contexts (e.g. `file://`).

---

## File Structure

```
bezpecne-heslo/
└── index.html   # entire application — HTML + CSS + JS in one file
```

No dependencies, no package.json, no build step.

---

## Language

The UI is in **Slovak**. Key terms:

| Slovak | English |
|---|---|
| Generovať | Generate |
| Kopírovať | Copy |
| Sila hesla | Password strength |
| Počet znakov | Character count |
| Počet číslic | Digit count |
| Počet špeciálnych znakov | Special character count |
| Vylúčiť podobné znaky | Exclude similar characters |
| Veľmi silné | Very strong |

---

## License

MIT — do whatever you want, just don't hold the author liable.
