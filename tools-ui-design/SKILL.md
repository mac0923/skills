---
name: tools-ui-design
description: Design-language spec for tool-style software. It covers a quiet, native-Mac-utility feel, neutral greys with a single indigo accent, compact typography, list cards, pill controls, frosted popovers and a monochrome silhouette logo, across light, dark, tray-panel, colorblind and marketing-site contexts. Use it when designing or restyling a tool, settings window, menu-bar or tray panel, developer app or dashboard, including its logo, app icon and website. Also use it when the user mentions "tools-ui-design" or asks for a restrained, native-Mac-tool look.
---

# tools-ui-design design language

In one sentence: **one quiet surface, real brand icons, and controls that read as system pop-up buttons.** The result should feel like a small native Mac utility, not a marketing web page. The interface stays visually quieter than the content, and every use of color needs a reason.

When designing with this spec, define the variables (colors, radii, font sizes) first, then build the components. Components reference only semantic variables and never hard-code color values, so switching theme means swapping one set of variables.

---

## 1. Principles

1. **Restraint.** Use large areas of neutral grey and a single accent color. Avoid decorative gradients, colored backgrounds and illustrations.
2. **Native feel.** Use the system font and system-like density and behavior (follow the HIG). Controls should look like macOS pop-up buttons, segmented controls and switches.
3. **Content is selectable, chrome is not.** Users can select and copy values, errors, logs and conversations. Buttons, labels, tabs and menus are chrome: they cannot be selected, and the cursor stays the default arrow over them.
4. **State is never color alone.** A failure changes shape (✕), not just a green dot turning red, so it stays readable for colorblind users and in greyscale.
5. **Motion explains space.** An element leaves the way it came in. All motion honors `prefers-reduced-motion`.
6. **Real brand icons.** Third-party items (providers, tools, agents) show their real logos, never generic placeholders.

---

## 2. Color

### 2.1 Semantic variables

| Variable | Light | Dark | Role |
|---|---|---|---|
| `--bg` | `#f4f4f6` | `#1a1a1e` | Window background, a slightly cool grey |
| `--card` | `#ffffff` | `#232327` | List cards, dialogs |
| `--card-2` | `#f9f9fb` | `#1f1f23` | Expanded editor area inside a card |
| `--pill` / `--pill-hover` | `#f1f1f4` / `#e9e9ee` | `#2d2d33` / `#36363d` | Control fill |
| `--line` | `#e3e3e8` | `#333339` | Card border |
| `--line-2` | `#ececf0` | `#2c2c32` | Row dividers inside a card, lighter than the border |
| `--fg` | `#1c1c21` | `#ededf1` | Primary text; also the color of the logo and of an "on" toggle |
| `--fg-2` | `#4b4b53` | `#b9b9c1` | Secondary body text |
| `--ctl-fg` | `#63636b` | `#a1a1aa` | Quiet text on controls, at least 4.5:1 contrast on every surface |
| `--muted` | `#85858d` | `#8b8b94` | Subtitles, descriptions |
| `--faint` | `#b9b9c2` | `#56565f` | Disabled, placeholder |
| `--accent` | `#4f46e5` | `#a5b4fc` | The only hue (indigo) |
| `--accent-fg` | `#ffffff` | `#14142a` | Text on the accent |
| `--accent-soft` | `#eeedfd` | `#2b2c47` | Soft accent background (badges, "new" hints) |
| `--sel` | `#ecebfb` | `#33345a` | Selected row |

**Status colors** each come with a soft background variant (`-soft`):

| | Light | Dark |
|---|---|---|
| Success (green) | `#189a58` / `#e4f6ec` | `#6fd99b` / `#1e3a2b` |
| Error (red) | `#d64545` / `#fbe9e9` | `#f28b82` / `#45272a` |
| Warning (amber) | `#b45309` / `#fbf0df` | `#f2b544` / `#3f3220` |

### 2.2 Color rules

- Every grey carries a faint blue-violet tint (e.g. `#1c1c21`, `#f4f4f6`), so the greys share a temperature with the indigo accent. Never use pure neutral grey.
- **Dark mode flips the accent's lightness.** Light mode uses deep indigo with white text. Dark mode uses the pale periwinkle `#a5b4fc` with dark text, rather than a brightened deep indigo. Status colors likewise switch to pastel versions in dark mode.
- The accent appears only on the primary button, focus rings, the outline of an open field, "new" dots, soft badges and checked checkboxes.
- An "on" toggle uses **ink (`--fg`)**, not the accent, so a column of toggles stays calm instead of reading as a row of blue lights.
- Only floating layers (popovers, dialogs) get shadows. Cards get a 1px hairline border and no shadow.

### 2.3 Charts and syntax highlighting

- Chart series, in order: indigo, sky, emerald, amber, pink, violet, slate. Light mode uses `#4f46e5 #0ea5e9 #10b981 #f59e0b #ec4899 #8b5cf6 #64748b`; dark mode uses the 300-level tints of the same hues.
- Colorblind mode switches to the Okabe–Ito palette (`#0072b2 #e69f00 #009e73 #d55e00 #cc79a7 #56b4e9`). Adjacent series must differ in both hue and lightness.
- Syntax highlighting: strings green, keywords violet, functions blue, numbers amber, values cyan, operators magenta, comments `--muted`.

---

## 3. Themes

| Theme | Trigger | Notes |
|---|---|---|
| Light | Default | See the table above |
| Dark | Follows the system; force it with `<html data-theme="dark">` | Background about `#1a1a1e`; cards one step lighter, popovers lighter still |
| Tray panel | Small popover opened from the menu bar | See below |
| Colorblind | Settings toggle | Changes only the chart palette; failure is always drawn as ✕ |
| Marketing site | Website | See section 9 |

The theme switcher has three options: **System / Light / Dark**, defaulting to System.

**The tray panel** sits on frosted glass (system vibrancy), and its own paint is only a thin tint:

- The background is 93% `--bg` mixed with transparent.
- Cards drop their border and use a 1px inset edge or shadow instead.
- Controls on this translucent backdrop are not grey fills. They are **white with a hairline edge and a 1px soft shadow**, so they read as real, pressable buttons.
- Rows compress to 40px.

The key to the theme model is that every component references only semantic variables. A theme is just a set of variable overrides, so adding one means changing no components.

---

## 4. Typography

- **Fonts:** use the system UI stack `-apple-system, "SF Pro Text", "Segoe UI", system-ui`. For Chinese, use Microsoft YaHei UI on Windows and PingFang on Mac. Monospace is `ui-monospace, "SF Mono", Menlo`, with Cascadia Mono on Windows.
- **Base:** 13px with 1.4 line height, and `-webkit-font-smoothing: antialiased`.
- **Size scale (in-app):**

| Size | Used for |
|---|---|
| 10.5–11px | Uppercase section labels, minor metadata |
| 11.5px | Row subtitles, status text, code |
| 12–12.5px | Control text, descriptive body |
| 13px | Row titles, base body |
| ~20px | KPI numbers |

- **Weights:** 400 for body text, 500 for row titles, 560 for badges and buttons, and 600 for the brand name and section labels. Never go above 600 in the app (the marketing site uses heavier weights).
- **Section labels:** 11px, weight 600, uppercase, `.05em` tracking, `--muted`.
- **Numbers:** always `font-variant-numeric: tabular-nums` so columns align.
- Row titles get slight negative tracking (`-.005em`) to look compact. Uppercase labels get positive tracking.

---

## 5. Shape and spacing

**Radius scale** (larger elements get larger radii):

| Radius | Elements |
|---|---|
| 2–4px | Inline code, checkboxes, small swatches |
| 6px | Fields, text buttons, segmented-control thumb |
| 7px | Icon buttons |
| 8px | Segmented-control frame |
| 10–11px | Popovers, cards inside the panel |
| 12px | List cards, tray panel window |
| 14px | Dialogs |
| 999px | Badges, toggles, avatars |

**Sizes:**

- Icon buttons are 26×26.
- Fields are 24–25px tall, bordered secondary buttons 27px, and segmented-control buttons 24px.
- List rows are at least 48px tall in a window and 40px in the panel, with slightly more padding on the left than the right (14 / 12).

**Spacing:** gaps mostly step between 4 and 12px, and the gap between an icon and its text is 9–12px. Overall density is close to a system settings pane, tighter than a typical web page.

---

## 6. Components

**Header bar.** The brand (logo plus lowercase name) sits on the left. A segmented control, absolutely centered, serves as the main navigation, and icon buttons (refresh, settings) sit on the right. The bar has no background and no bottom border.

**Segmented control (main navigation tabs).** There is no grey track; only the active item's thumb shows.

- In light mode the thumb is white with a hairline shadow `0 1px 2px rgba(0,0,0,.14), 0 0 0 .5px rgba(0,0,0,.08)`.
- In dark mode the thumb is `rgba(255,255,255,.15)` with a 0.5px top highlight.
- Inactive items use `--ctl-fg` and darken one step on hover. The active item uses `--fg`.

**List card.** Group similar items into a single `--card` card instead of a separate card per item. The card has a 12px radius and a 1px `--line` border, and its rows are separated by `--line-2`. A row reads left to right:

```
[brand icon 22px]  Name (500)                         [field ▾]  [toggle]
                   ● subtitle (11.5px, --muted)
```

The card can end with a centered "Show N more ⌄" text button.

**Field (pop-up button).** A `--pill` fill with a 6px radius and 25px height, with no border. It shows a brand icon and the value on the left and a small ⌄ on the right. While open, it gets a 1px accent inset outline.

**Buttons** come in three tiers:

- **Primary:** accent fill, `--accent-fg` text, weight 500. On hover it only brightens (`brightness(1.08)`) and does not change color.
- **Secondary:** `--card` background with a 1px `--line` border and a barely visible shadow `0 1px 1px rgba(0,0,0,.04)`. On hover the border turns `--muted`.
- **Text:** no background and `--ctl-fg` text; a `--pill` background appears on hover. A destructive button looks like a normal text button until hover, when it shows red text on a red soft background.

**Icon button.** 26px square with a 7px radius, `--muted` at rest. On hover or when active, a `--pill` background appears and the icon turns `--fg`.

**Toggle.** A capsule of about 34×20. The track is `--faint` when off and `--fg` when on (near-black in light mode, near-white in dark). The knob uses the surface color, with a fine edge and a soft drop shadow.

**Status dot.** A 6px circle: green for success, amber for warning. A failure is **drawn as an ✕** (a mask swaps the dot for a cross), not just turned red.

**Badge** (e.g. "Update ready"). A 22px-tall capsule (999px radius) with accent text on `--accent-soft`, plus a 0.5px semi-transparent accent inset edge. On hover it inverts to a solid accent fill.

**"New" dot.** A 6px accent dot. When it appears it springs in, then sends out a single ripple ring, only once.

**Popover.** A translucent `--pop-bg` (white at 94% in light mode, 96% in dark) with a 24px backdrop blur and an 11px radius. Its shadow has three layers: a wide soft shadow, a close shadow and a 0.5px edge.

**Dialog.** A `--card` surface with a 14px radius, a 1px `--line` ring and a deep shadow `0 24px 60px rgba(0,0,0,.32)`. It defaults to 600px wide and grows up to 880px when the content needs room. The header and button bars stay fixed and only the middle scrolls.

**KPI tiles.** The tiles sit in a grid with 1px gaps, and `--line` showing through the gaps forms the dividers. Each tile has a small uppercase label above a large tabular number.

**Footer preset bar.** An uppercase label (e.g. PROFILES) on the left, followed by capsule preset buttons (a name plus an accent dot), with a "+ Save current" text button on the right.

---

## 7. Motion

- One easing curve, `cubic-bezier(.2, .8, .2, 1)`: a quick start and a soft finish.
- Color and background transitions take .12s; segmented-control switches take .18s.
- **Popovers grow out of the button that opened them.** Set `transform-origin` to the button's midpoint and animate from `translateY(-6px) scale(.94)` to rest over .42s with `cubic-bezier(.16,1,.3,1)`. There is no bounce, in the manner of iOS menus. Opacity finishes first, within .18s. On close, the popover fades out first and shrinks back toward the button over .22s.
- Press feedback is `scale(.96)` or `translateY(1px)`.
- Spinners rotate the graphic inside the SVG, not the whole element, to avoid jitter from WebKit's pixel snapping.
- With "Reduce motion" on, keep only fades and drop all translation and scaling.

---

## 8. Logo and app-icon design language

### 8.1 Logo form

- **Subject:** a real animal or object tied to the product name, drawn as a **side-profile silhouette facing right** (the reading direction, which suggests moving forward). Prefer an animal: it carries more character and is more memorable than abstract geometry.
- **Solid monochrome:** the whole logo is **one compound path in one color**, with no strokes, gradients, shadows or outlines. Every interior detail is carved out as **negative space**:
  - The subject's most distinctive feature (markings, a color patch, a wing) becomes a large negative shape that creates black-and-white contrast.
  - The eye is a small round hole that brings the silhouette to life.
  - The extremities (tail, feathers, fur) are split by a few thin slits into 2–3 fanned strands.
- **Pose and composition:**
  - On a square grid (44×44), the subject spans almost the full width, with about 1/8 empty space above and below.
  - The extremity sweeps up diagonally toward the upper left, for momentum.
  - The body is round and bottom-weighted, for stability.
  - The head's point (beak, nose, ear) is short and sharp and aims up and to the right.
- **Line quality:** organic curves with a slight woodcut or print-making feel. Extremities end in sharp points while the body contour is a full curve, and the contrast between points and curves gives the mark its character.
- **Two levels of detail:**
  - The full version, for 32px and up, keeps every slit and small accent.
  - The small version, for 14–24px (header bar, tray, favicon), has fewer nodes and merges small negative shapes. It keeps only the silhouette, the main negative shapes and the eye.
- **Recognition test:** at 16px with all color removed, the subject is still recognizable at a glance.

### 8.2 Logo color and pairing

- The logo uses **ink only**, the primary text color `--fg`, and **never the accent**, which would compete with the adjacent text. When the theme switches, the logo inverts along with the text.
- The favicon carries its own light and dark variants: `#1c1c1e` in light mode and `#f2f2f2` in dark.
- Third-party brand icons keep their original colors if they are color logos. Monochrome logos take the current text color and follow the theme.

### 8.3 Wordmark

- The product name is **all lowercase** in the system font, with no custom typeface.
- In the app: 18px logo, 6px gap, weight 600, `.01em` tracking.
- In the website nav: 24px logo, 9px gap, 17px text, weight 650, `-.01em` tracking.

### 8.4 App icon

- A macOS squircle with a **very light vertical gradient** behind:
  - Light: from pure white to `#ececec`.
  - Dark: from `#3a3a3a` to `#222222`.
- A centered monochrome silhouette fills about 75% of the squircle's width. It is near-black `#161616` in light mode and near-white `#f4f4f4` in dark.
- It has a neutral shadow at about 50% opacity, and translucency is off.
- There is no gloss, highlight, outline or second color. The icon is simply **a silhouette on a sheet of paper**.

### 8.5 Logo motion

- At rest the logo is drawn as one piece. To animate, it splits into three moving parts: the **appendage** (wing, arm, ear), the **extremity** (tail) and the **body**. Each part rotates around its own joint, and they are reassembled into one piece afterward so the cuts never show.
- The animation plays once when the window opens and on hover. It lasts .9s with `cubic-bezier(.3,0,.3,1)`, and every part follows a damped oscillation:
  - Appendage swing: +10° → −3° → +8° → −2° → +3° → 0
  - Extremity flick: +16° → −7° → +9° → −3° → +2° → 0
  - Body bob: −4° → +2° → −1° → 0
- Settings can turn off the logo animation on its own, and it does not play when "Reduce motion" is on.

---

## 9. Marketing site

The site is **more black-and-white** than the app: the accent disappears too, leaving only ink and paper.

- **Colors:**
  - Background: `#fafafa` in light mode and `#0b0b0c` in dark, which is deeper than the app's dark background.
  - Cards: white in light mode, `#161618` in dark.
  - Lines: `#e4e4e7` in light mode, `#26262a` in dark.
- **Buttons:** the primary button is an **inverted ink block**, black on white in light mode and white on black in dark. It is 42px tall with a 10px radius and weight 560, and on hover it lowers its opacity. The secondary button is transparent with a hairline border.
- **Headline:** 40–64px, weight 700, line height 1.04, `-.035em` tracking (very tight). The second half of the headline is dimmed to the tertiary grey (`--ink3`), giving a "claim + qualifier" rhythm.
- **Other type:**
  - The lede is 19px in the secondary grey, at most 30em wide.
  - Section eyebrows are 13px, uppercase, `.08em` tracking, in the tertiary grey.
  - H2 is 30–42px, weight 680.
- **Layout:** content is at most 1080px wide, and sections are 88px apart. The hero has text on the left and an image on the right, in about a 1.05 : 0.95 ratio.
- **Navigation:** a sticky bar with a frosted background, 78% of the background color plus `saturate(1.4) blur(14px)`. Its bottom border appears only after scrolling.
- **Product screenshots:** 14px radius, 1px border and a long soft shadow. Provide **one light and one dark capture**, switched to match the theme.
- **Feature grid:** 3–4 columns. The 1px gaps let the background show through as dividers. The outer frame has a 16px radius and each cell has 28px padding.
- **Supported tools/agents:** a centered row of 22px icons with names, under a small uppercase heading.
- **Chinese and Japanese:** relax headline tracking to `-.01em` and uppercase-style labels to `.04em`. Japanese uses a Japanese font stack and never borrows the Chinese fonts.

---

## 10. Checklist

- [ ] Apart from status colors, the interface has only one hue.
- [ ] Every color references a semantic variable, and no hard-coded color shows up after switching to dark.
- [ ] In dark mode the accent is light, with dark text on it.
- [ ] Similar items are grouped in one list card, not scattered across many small cards.
- [ ] Only floating layers have shadows.
- [ ] Failure states are recognizable in greyscale.
- [ ] Numbers use tabular figures.
- [ ] The logo is ink, not the accent.
- [ ] With "Reduce motion" on, there is no translation or scaling animation.
- [ ] Chrome text is not selectable; content text is.
