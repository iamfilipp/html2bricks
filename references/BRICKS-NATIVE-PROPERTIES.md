# Bricks Native Properties Reference

**Verified against Bricks 2.3.5 via live MCP**

## Critical Gotchas First

1. **`_textAlign` does nothing** — text-align goes inside `_typography`
2. **`_gap` / `_display` don't work on layout elements** — section/container/block/div are always flex; for gap use `_cssCustom: "#brxe-id { gap: 24px; }"`
3. **`_widthMax` not `_maxWidth`** — naming pattern: `_[property][Min/Max]`
4. **Gradient = plain CSS string** — `{"gradient": "linear-gradient(...)"}` not stops array
5. **`%root%` does nothing** — use `#brxe-{elementId}` in `_cssCustom`

---

## Layout / Spacing

```json
"_padding": {"top": "80", "right": "16", "bottom": "80", "left": "16"}
"_padding": "40px 0"                         // Shorthand string also works
"_margin": {"top": "0", "right": "auto", "bottom": "0", "left": "auto"}
"_gap": "16"                                 // ⚠️ Non-layout elements only
```

### Dimensions

Pattern: `_[property][Min/Max]` — NOT `_[min/max][Property]`

```json
"_width": "100%"
"_widthMin": "320"
"_widthMax": "1200"
"_height": "500"
"_heightMin": "100vh"
"_heightMax": "800"
```

✅ `"_widthMax"` ❌ `"_maxWidth"`
✅ `"_heightMin"` ❌ `"_minHeight"`

---

## Display & Position

```json
"_display": "flex"           // ⚠️ Non-layout elements only (layout = always flex)
"_position": "relative"      // static, relative, absolute, fixed, sticky
"_top": "0"
"_right": "0"
"_bottom": "0"
"_left": "0"
"_zIndex": "10"
"_overflow": "hidden"        // visible, hidden, scroll, auto
"_overflowX": "auto"
"_overflowY": "scroll"
"_visibility": "visible"     // visible, hidden
"_cursor": "pointer"
```

---

## Flexbox (non-layout elements, or via _cssCustom for layout elements)

```json
"_display": "flex"
"_direction": "row"                // row, row-reverse, column, column-reverse
"_alignItems": "center"            // flex-start, flex-end, center, baseline, stretch
"_justifyContent": "space-between" // flex-start, flex-end, center, space-between, space-around, space-evenly
"_flexWrap": "wrap"                // nowrap, wrap, wrap-reverse
"_gap": "20"                       // ⚠️ Use _cssCustom for section/container/block/div
```

**For layout elements (section/container/block/div) — use `_cssCustom`:**
```json
"_cssCustom": "#brxe-abc123 { gap: 24px; flex-direction: row; }"
```

---

## Grid

```json
"_display": "grid"
"_gridTemplateColumns": "repeat(3, 1fr)"
"_gridTemplateRows": "auto"
"_gridGap": "20"
"_gridColumnGap": "20"
"_gridRowGap": "20"
```

---

## Typography

```json
"_typography": {
  "font-family": "Arial, sans-serif",
  "font-size": "16",
  "font-weight": "600",
  "line-height": "1.5",
  "letter-spacing": "0.5",
  "text-align": "center",          // ← text-align goes HERE (not _textAlign)
  "text-transform": "uppercase",
  "text-decoration": "underline",
  "color": {"hex": "#000000"},
  "font-style": "italic"
}
```

**⚠️ `_textAlign` does nothing** — always put `text-align` inside `_typography`.

---

## Background

### Solid Color
```json
"_background": {
  "color": {"hex": "#0066cc"}
}
```

### Image
```json
"_background": {
  "image": {
    "url": "https://...",
    "external": true,
    "size": "cover",       // cover, contain, auto
    "position": "center center",
    "repeat": "no-repeat"  // repeat, no-repeat, repeat-x, repeat-y
  }
}
```

### Gradient (plain CSS string — not stops array)
```json
"_background": {
  "gradient": "linear-gradient(135deg, #667eea 0%, #764ba2 100%)"
}
```

```json
"_background": {
  "gradient": "radial-gradient(circle, #f093fb 0%, #f5576c 100%)"
}
```

**⚠️ Gradient is a plain CSS string.** Previous versions documented a stops array — that was wrong.

---

## Border

```json
"_border": {
  "style": "solid",
  "width": {"top": "1", "right": "1", "bottom": "1", "left": "1"},
  "color": {"hex": "#cccccc"},
  "radius": {"top": "8", "right": "8", "bottom": "8", "left": "8"}
}
```

**Border radius shorthand:**
```json
"_borderRadius": {
  "topLeft": "8",
  "topRight": "8",
  "bottomRight": "8",
  "bottomLeft": "8"
}
```

For circles: `"50%"` for all corners.

---

## Effects

### Box Shadow
```json
"_boxShadow": [
  {
    "offsetX": "0",
    "offsetY": "4",
    "blur": "16",
    "spread": "0",
    "color": {"hex": "#000000", "opacity": 0.1}
  }
]
```

### Transform
```json
"_transform": {
  "translateX": "10",
  "translateY": "-5",
  "scaleX": "1.1",
  "scaleY": "1.1",
  "rotate": "45",
  "skewX": "0",
  "skewY": "0"
}
```

**⚠️ Complex combined transforms** (e.g. `rotate(45deg) translateY(-420px)`) — use `_cssCustom`:
```json
"_cssCustom": "#brxe-id { transform: rotate(45deg) translateY(-420px); }"
```

### Opacity & Transition
```json
"_opacity": "0.8"
"_cssTransition": "all 0.3s ease"
```

---

## Native Parallax (Bricks 2.3+)

Set directly in element settings — no JavaScript needed.

```json
// Move element while scrolling
"_motionElementParallax": true,
"_motionElementParallaxSpeedX": 0,
"_motionElementParallaxSpeedY": -20,
"_motionStartVisiblePercent": 0
```

```json
// Move background image while scrolling
"_motionBackgroundParallax": true,
"_motionBackgroundParallaxSpeed": -15,
"_motionStartVisiblePercent": 0
```

- Speed = percentage. Negative = opposite scroll direction.
- `_motionStartVisiblePercent`: 0 = element entering viewport, 50 = near center.
- Not visible in builder — only on live frontend.

---

## _cssCustom — Use `#brxe-{id}` Selector

```json
"_cssCustom": "#brxe-einrji { transform: rotate(45deg); }"
"_cssCustom": "#brxe-einrji { gap: 32px; flex-direction: row; }"
"_cssCustom": "#brxe-einrji { mix-blend-mode: overlay; }"
"_cssCustom": "#brxe-einrji:hover .child-class { opacity: 1; }"
```

**⚠️ NOT `%root%`** — that does nothing via API.

Multiple rules:
```json
"_cssCustom": "#brxe-einrji { gap: 24px; } #brxe-einrji:hover { opacity: 0.9; }"
```

---

## Common Pitfalls

### Zero Dimensions Collapse
Elements with `width: 0` + `height: 0` collapse. Absolutely positioned children need a dimensioned parent.

✅ Use a real dimension:
```json
{"_position": "relative", "_width": "100%", "_height": "400"}
```

### Property Name Pattern
`_[property][Min/Max]` not `_[min/max][Property]`:
- `_width` / `_widthMin` / `_widthMax`
- `_height` / `_heightMin` / `_heightMax`

### Layout Elements and Gap
Section/Container/Block/Div are always flex. `_gap` and `_display` don't apply. Use:
```json
"_cssCustom": "#brxe-abc123 { gap: 24px; }"
```
