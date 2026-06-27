# iOS Visual Language for HTML Prototypes

Use these conventions when the UI prototype target is a native iOS screen. Treat this as the project's styling system in place of any web framework.

## Device Frame

Render inside a 390×844px container (iPhone 15 Pro logical size). Wrap the device in a neutral background so the phone boundary is obvious.

```css
:root {
  --safe-top: 59px;    /* Dynamic Island + status bar */
  --safe-bottom: 34px; /* home indicator */
  --nav-bar-height: 44px;
  --tab-bar-height: 49px;
}

body {
  width: 390px;
  min-height: 844px;
  margin: 0 auto;
  font-family: -apple-system, 'SF Pro Text', 'SF Pro Display', system-ui, sans-serif;
  -webkit-font-smoothing: antialiased;
  background: var(--color-bg-primary);
  color: var(--color-label);
  overflow-x: hidden;
}
```

## Color System

```css
:root {
  --color-bg-primary: #FFFFFF;
  --color-bg-secondary: #F2F2F7;
  --color-bg-tertiary: #FFFFFF;
  --color-bg-grouped: #F2F2F7;
  --color-bg-grouped-secondary: #FFFFFF;

  --color-label: #000000;
  --color-label-secondary: rgba(60, 60, 67, 0.60);
  --color-label-tertiary: rgba(60, 60, 67, 0.30);
  --color-label-quaternary: rgba(60, 60, 67, 0.18);

  --color-fill: rgba(120, 120, 128, 0.20);
  --color-fill-secondary: rgba(120, 120, 128, 0.16);
  --color-fill-tertiary: rgba(118, 118, 128, 0.12);

  --color-separator: rgba(60, 60, 67, 0.29);
  --color-separator-opaque: #C6C6C8;

  --color-blue:   #007AFF;
  --color-red:    #FF3B30;
  --color-green:  #34C759;
  --color-orange: #FF9500;
  --color-yellow: #FFCC00;
  --color-teal:   #30B0C7;
  --color-indigo: #5856D6;
  --color-purple: #AF52DE;
  --color-pink:   #FF2D55;
}

@media (prefers-color-scheme: dark) {
  :root {
    --color-bg-primary: #000000;
    --color-bg-secondary: #1C1C1E;
    --color-bg-tertiary: #2C2C2E;
    --color-bg-grouped: #1C1C1E;
    --color-bg-grouped-secondary: #2C2C2E;

    --color-label: #FFFFFF;
    --color-label-secondary: rgba(235, 235, 245, 0.60);
    --color-label-tertiary: rgba(235, 235, 245, 0.30);
    --color-label-quaternary: rgba(235, 235, 245, 0.18);

    --color-fill: rgba(120, 120, 128, 0.36);
    --color-fill-secondary: rgba(120, 120, 128, 0.32);
    --color-fill-tertiary: rgba(118, 118, 128, 0.24);

    --color-separator: rgba(84, 84, 88, 0.65);
    --color-separator-opaque: #38383A;

    --color-blue:   #0A84FF;
    --color-red:    #FF453A;
    --color-green:  #30D158;
    --color-orange: #FF9F0A;
    --color-yellow: #FFD60A;
    --color-teal:   #40CBE0;
    --color-indigo: #5E5CE6;
    --color-purple: #BF5AF2;
    --color-pink:   #FF375F;
  }
}
```

## Typography Scale

Maps to iOS Dynamic Type at default size. Use `px`, not `rem` — iOS does not scale with browser zoom.

| Style | Size | Weight | Line height |
|---|---|---|---|
| Large Title | 34px | 700 | 41px |
| Title 1 | 28px | 700 | 34px |
| Title 2 | 22px | 700 | 28px |
| Title 3 | 20px | 600 | 25px |
| Headline | 17px | 600 | 22px |
| Body | 17px | 400 | 22px |
| Callout | 16px | 400 | 21px |
| Subhead | 15px | 400 | 20px |
| Footnote | 13px | 400 | 18px |
| Caption 1 | 12px | 400 | 16px |
| Caption 2 | 11px | 400 | 13px |

```css
.text-large-title { font-size: 34px; font-weight: 700; line-height: 41px; }
.text-title1      { font-size: 28px; font-weight: 700; line-height: 34px; }
.text-title2      { font-size: 22px; font-weight: 700; line-height: 28px; }
.text-title3      { font-size: 20px; font-weight: 600; line-height: 25px; }
.text-headline    { font-size: 17px; font-weight: 600; line-height: 22px; }
.text-body        { font-size: 17px; font-weight: 400; line-height: 22px; }
.text-callout     { font-size: 16px; font-weight: 400; line-height: 21px; }
.text-subhead     { font-size: 15px; font-weight: 400; line-height: 20px; }
.text-footnote    { font-size: 13px; font-weight: 400; line-height: 18px; }
.text-caption1    { font-size: 12px; font-weight: 400; line-height: 16px; }
.text-caption2    { font-size: 11px; font-weight: 400; line-height: 13px; }
```

## Spacing

8pt grid. Standard content margin: `16px`. Grouped list section inset: `16px`.

```css
:root {
  --space-4:  4px;
  --space-8:  8px;
  --space-12: 12px;
  --space-16: 16px;
  --space-20: 20px;
  --space-24: 24px;
  --space-32: 32px;
  --space-44: 44px; /* minimum touch target */
}
```

## Touch Targets

Every tappable element must be at least 44×44px effective hit area.

```css
.tappable {
  min-height: 44px;
  min-width: 44px;
  display: flex;
  align-items: center;
}
```

## Corner Radii

| Context | Radius |
|---|---|
| Badges, chips | 6px |
| List cells (grouped) | 10px |
| Cards | 12px |
| Large cards, bottom sheets | 16px |
| Buttons (pill) | 9999px |

## Navigation Bar

Standard (inline title):

```css
.nav-bar {
  position: sticky;
  top: var(--safe-top);
  height: var(--nav-bar-height);
  background: var(--color-bg-primary);
  border-bottom: 0.5px solid var(--color-separator);
  display: flex;
  align-items: center;
  padding: 0 16px;
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  z-index: 10;
}

.nav-bar-title {
  font-size: 17px;
  font-weight: 600;
  flex: 1;
  text-align: center;
}

.nav-bar-button {
  font-size: 17px;
  color: var(--color-blue);
  background: none;
  border: none;
  padding: 0;
  min-width: 44px;
  min-height: 44px;
  display: flex;
  align-items: center;
  cursor: pointer;
}
```

Large-title nav bar (collapses on scroll): place the title in the content area at `font-size: 34px; font-weight: 700` above the first section, use a transparent/blurred nav bar with no inline title until the content title scrolls past.

## Tab Bar

```css
.tab-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: calc(var(--tab-bar-height) + var(--safe-bottom));
  padding-bottom: var(--safe-bottom);
  background: var(--color-bg-primary);
  border-top: 0.5px solid var(--color-separator);
  display: flex;
  backdrop-filter: saturate(180%) blur(20px);
  -webkit-backdrop-filter: saturate(180%) blur(20px);
  z-index: 10;
}

.tab-bar-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 3px;
  color: var(--color-label-secondary);
  font-size: 10px;
  cursor: pointer;
}

.tab-bar-item.active {
  color: var(--color-blue);
}
```

SF Symbols are not available in HTML — approximate with Unicode or inline SVG, not emoji.

## Inset Grouped List (most common list style)

```css
.list-section {
  margin: 0 16px;
  background: var(--color-bg-grouped-secondary);
  border-radius: 10px;
  overflow: hidden;
}

.list-section + .list-section {
  margin-top: 20px;
}

.list-section-header {
  font-size: 13px;
  font-weight: 400;
  color: var(--color-label-secondary);
  text-transform: uppercase;
  letter-spacing: 0.06em;
  padding: 0 16px 6px;
  margin-top: 24px;
}

.list-cell {
  min-height: 44px;
  padding: 11px 16px;
  display: flex;
  align-items: center;
  gap: 12px;
  background: var(--color-bg-grouped-secondary);
  position: relative;
  cursor: pointer;
}

.list-cell + .list-cell::before {
  content: '';
  position: absolute;
  top: 0;
  left: 16px;
  right: 0;
  height: 0.5px;
  background: var(--color-separator);
}

.list-cell-label {
  flex: 1;
  font-size: 17px;
  color: var(--color-label);
}

.list-cell-value {
  font-size: 17px;
  color: var(--color-label-secondary);
}

/* Disclosure chevron */
.list-cell-chevron::after {
  content: '›';
  font-size: 18px;
  color: var(--color-label-tertiary);
  margin-left: 4px;
}
```

## Buttons

```css
.btn-filled {
  background: var(--color-blue);
  color: #FFFFFF;
  font-size: 17px;
  font-weight: 600;
  padding: 14px 20px;
  border-radius: 14px;
  border: none;
  width: 100%;
  cursor: pointer;
  text-align: center;
}

.btn-tinted {
  background: rgba(0, 122, 255, 0.12);
  color: var(--color-blue);
  font-size: 17px;
  font-weight: 600;
  padding: 14px 20px;
  border-radius: 14px;
  border: none;
  width: 100%;
  cursor: pointer;
  text-align: center;
}

.btn-destructive {
  background: var(--color-red);
  color: #FFFFFF;
  font-size: 17px;
  font-weight: 600;
  padding: 14px 20px;
  border-radius: 14px;
  border: none;
  width: 100%;
  cursor: pointer;
  text-align: center;
}

.btn-plain {
  background: none;
  color: var(--color-blue);
  font-size: 17px;
  font-weight: 400;
  border: none;
  cursor: pointer;
  padding: 11px 0;
}
```

## Search Bar

```css
.search-bar {
  display: flex;
  align-items: center;
  background: var(--color-fill-tertiary);
  border-radius: 10px;
  padding: 7px 8px;
  gap: 6px;
  margin: 8px 16px;
}

.search-bar-input {
  flex: 1;
  background: none;
  border: none;
  font-size: 17px;
  font-family: inherit;
  color: var(--color-label);
  outline: none;
}

.search-bar-input::placeholder {
  color: var(--color-label-tertiary);
}
```

## Segmented Control

```css
.segmented-control {
  display: flex;
  background: var(--color-fill-tertiary);
  border-radius: 9px;
  padding: 2px;
  margin: 0 16px;
}

.segmented-segment {
  flex: 1;
  text-align: center;
  padding: 6px 0;
  border-radius: 7px;
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  color: var(--color-label);
}

.segmented-segment.active {
  background: var(--color-bg-primary);
  box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.08);
}
```

## Shadows

iOS shadows are very subtle — never use large offsets or heavy opacity.

```css
:root {
  --shadow-sm: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.08);
  --shadow-md: 0 4px 16px rgba(0,0,0,0.12);
  --shadow-lg: 0 8px 30px rgba(0,0,0,0.15);
}
```

## Anti-patterns

- **Don't use web color names** (`blue`, `red`) — use `--color-*` variables so dark mode works
- **Don't use `rem`** — use `px`; iOS doesn't scale with browser zoom
- **Don't use hover states as the primary affordance** — iOS is touch-first; show pressed state with `opacity: 0.6` or a background tint instead
- **Don't use web link conventions** (underlined links in body text, blue anchor default) — they look foreign on iOS
- **Don't skip safe areas** — content behind the Dynamic Island or home indicator looks immediately wrong
- **Don't use `box-shadow` with large offsets** — iOS uses extremely subtle shadows; large offsets signal "web Material Design"
- **Don't use `1px` borders** — iOS uses `0.5px` hairlines for separators; `1px` is visibly chunky on retina
- **SF Symbols are unavailable** in HTML — approximate with Unicode or inline SVG; never use emoji as system icons

## Checklist Before Handing Off

- [ ] All content is inset below `--safe-top` and above `--safe-bottom`
- [ ] All tappable elements are at least 44×44px
- [ ] Dark mode variables are defined and render correctly (`@media prefers-color-scheme: dark`)
- [ ] Font is `-apple-system` throughout
- [ ] Separators use `0.5px` not `1px`
- [ ] No hover-only affordances
- [ ] Nav bar and/or tab bar present if the screen would have them in native
