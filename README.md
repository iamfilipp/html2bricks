# h2b — HTML to Bricks Builder Converter

(Claude AI Skill)

**Version 4.0.0** | 166+ Elements | Bricks 2.3.5 | MCP-Verified

Convert HTML, CSS, and JavaScript to Bricks Builder paste-ready JSON. Flat structure, ID-based relationships, 99.5%+ native property coverage, full interactions and conditions support.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## What's New in v4.0.0

**MCP-verified against live Bricks 2.3.5 instance. Major corrections and new features:**

- ✅ **`_cssCustom` works** — previous versions said it didn't. Use `#brxe-{id}` as selector (not `%root%`)
- ✅ **166+ elements** — expanded from 31, all categories catalogued with correct `name` slugs
- ✅ **Full interactions schema** — every trigger, action, and field name verified from live API
- ✅ **New: Element Conditions** — complete `_conditions` schema with 20+ condition keys
- ✅ **New: Native Parallax** — `_motionElementParallax` / `_motionBackgroundParallax` (Bricks 2.3+)
- ✅ **Gradient format corrected** — plain CSS string, not stops array
- ✅ **`_textAlign` gotcha documented** — does nothing; `text-align` goes inside `_typography`
- ✅ **Layout element gap fixed** — `_gap`/`_display` don't apply to section/container/block/div; use `_cssCustom`
- ✅ **Bricks version** — updated from 2.1.4 to 2.3.5

See [CHANGELOG.md](CHANGELOG.md) for full details.

---

## Quick Start

### Install as Claude Skill

1. Download `h2b.skill`
2. Claude.ai → Settings → Skills → Upload
3. Prompt: _"Convert this HTML to Bricks JSON"_ or _"Build this component in Bricks"_

### Manual Use

Copy any JSON from `examples/` directly into Bricks Builder via **Cmd+V** on canvas.

---

## Key Features

- **Flat structure** — ID-based parent/children, never nested objects
- **166+ elements** — Basic, Layout, General, Media, Single, WP, Filter, WooCommerce, Product
- **Pseudo-selectors** — `:hover`, `:focus`, `:nth-child` natively
- **Interactions** — Full `_interactions` array with all 16 triggers and 17 actions
- **Element Conditions** — `_conditions` for server-side show/hide (user role, date, ACF, WooCommerce)
- **Native Parallax** — no JS needed (Bricks 2.3+)
- **99.5%+ CSS coverage** — with `_cssCustom` for anything without a native property

---

## Flat Structure

```json
{
  "content": [
    {"id": "mhkwpa", "name": "section", "parent": 0, "children": ["qnxrtb"], "settings": {}, "label": "Hero"},
    {"id": "qnxrtb", "name": "container", "parent": "mhkwpa", "children": ["einrji"], "settings": {}, "label": "Wrapper"},
    {"id": "einrji", "name": "heading", "parent": "qnxrtb", "children": [], "settings": {"tag": "h1", "text": "Hello"}, "label": "Title"}
  ],
  "source": "bricksCopiedElements",
  "sourceUrl": "https://github.com/iamfilipp/html2bricks",
  "version": "2.3.5",
  "globalClasses": [],
  "globalElements": []
}
```

**Required fields on every element:** `id` · `name` · `parent` · `children` · `settings` · `label`

**ID format:** Random 6-char lowercase alphanumeric (e.g. `einrji`, `mhkwpa`)

---

## Layout Elements — Decision Guide

| Need | Element | Width | Display |
|------|---------|-------|---------|
| Root page region | `section` | 100% | flex |
| Centered max-width wrapper | `container` | 1100px | flex |
| Flex column / row | `block` | 100% | flex |
| Decorative / absolute / unstyled | `div` | auto | block |

---

## `_cssCustom` — The Right Way

`_cssCustom` works. Use `#brxe-{elementId}` as the selector — **not** `%root%`.

```json
{
  "id": "einrji",
  "name": "div",
  "settings": {
    "_cssCustom": "#brxe-einrji { transform: rotate(45deg); mix-blend-mode: overlay; }"
  }
}
```

**Use `_cssCustom` for:** complex transforms · `mix-blend-mode` · `gap` on layout elements · complex selectors (`.parent:hover .child`)

---

## Critical Gotchas

| ❌ Wrong | ✅ Correct |
|----------|-----------|
| `"_textAlign": "center"` | `"_typography": {"text-align": "center"}` |
| `"_maxWidth": "1200"` | `"_widthMax": "1200"` |
| `"_gap": "24"` on section/container | `"_cssCustom": "#brxe-id { gap: 24px; }"` |
| `"_cssCustom": "%root% { ... }"` | `"_cssCustom": "#brxe-{id} { ... }"` |
| Gradient stops array | `"gradient": "linear-gradient(135deg, #667eea, #764ba2)"` |
| `"_animation": "fadeIn"` | `"_interactions": [{...}]` |

---

## Interactions

Stored in `settings._interactions` as an array. Each interaction needs a unique 6-char ID.

```json
"_interactions": [
  {
    "id": "aa1bb2",
    "trigger": "enterView",
    "action": "startAnimation",
    "animationType": "fadeInUp",
    "animationDuration": "0.8s",
    "animationDelay": "0s",
    "target": "self",
    "runOnce": true,
    "rootMargin": "0px 0px -80px 0px"
  }
]
```

**Triggers:** `click` · `mouseenter` · `mouseleave` · `enterView` · `leaveView` · `contentLoaded` · `scroll` · `mouseleaveWindow` · `animationEnd` · `formSubmit` · `formSuccess` · `formError` · `ajaxStart` · `ajaxEnd`

**Actions:** `startAnimation` · `show` · `hide` · `setAttribute` · `toggleAttribute` · `toggleOffCanvas` · `loadMore` · `loadMoreGallery` · `scrollTo` · `javascript` · `clearForm` · and more

**Animate.css types (selection):** `fadeInUp` · `fadeInDown` · `fadeIn` · `zoomIn` · `slideInLeft` · `bounceIn` · `pulse` — [full list in INTERACTIONS.md](references/INTERACTIONS.md)

---

## Element Conditions

Server-side show/hide logic. Stored in `settings._conditions`.
Outer array = OR, inner array = AND.

```json
"_conditions": [
  [{"key": "user_logged_in", "compare": "==", "value": "1"}]
]
```

**Available keys:** `user_logged_in` · `user_role` · `user_id` · `post_id` · `post_status` · `featured_image` · `date` · `time` · `weekday` · `dynamic_data` · `browser` · `current_url` · WooCommerce keys ([full list in CONDITIONS.md](references/CONDITIONS.md))

---

## Native Parallax (Bricks 2.3+)

No JavaScript needed. Set as style properties directly on the element:

```json
{
  "_motionElementParallax": true,
  "_motionElementParallaxSpeedY": -20,
  "_motionStartVisiblePercent": 0
}
```

```json
{
  "_motionBackgroundParallax": true,
  "_motionBackgroundParallaxSpeed": -15,
  "_motionStartVisiblePercent": 0
}
```

Speed = percentage. Negative = opposite scroll direction.

---

## Property Naming Pattern

`_[property][Min/Max]` — not `_[min/max][Property]`

```json
"_widthMin": "320"    ✅
"_widthMax": "1200"   ✅
"_heightMin": "100vh" ✅
"_minWidth": "320"    ❌
"_maxWidth": "1200"   ❌
```

---

## Coverage

**Native (99.5%+):** Layout · Flexbox · Grid · Typography · Background · Border · Effects · Transform · Transitions · Parallax · Interactions · Conditions

**Needs `_cssCustom`:** complex multi-operation transforms · `mix-blend-mode` · `gap` on layout elements

**External CSS only:** `@keyframes` · `::before` / `::after` · attribute selectors

---

## Documentation

The skill includes 6 reference guides:

| File | Contents |
|------|---------|
| `BRICKS-ELEMENTS.md` | 166+ elements with names, categories, HTML mapping |
| `BRICKS-NATIVE-PROPERTIES.md` | All native properties with correct key names |
| `INTERACTIONS.md` | Full interactions schema — triggers, actions, Animate.css types, patterns |
| `CONDITIONS.md` | Element conditions schema — all keys, operators, examples |
| `PSEUDO-SELECTORS.md` | Pseudo-selector conversion guide |
| `JAVASCRIPT-HANDLING.md` | JavaScript processing strategy |

---

## Examples

- **[01-simple-hero](examples/01-simple-hero/)** — Hero section with scroll reveal animation

---

## Author

**Filipp Gavrilos** / Mobian Studio
GitHub: [@iamfilipp](https://github.com/iamfilipp) | [mobians.co](https://mobians.co)

---

## License

MIT — see [LICENSE](LICENSE)

---

**h2b v4.0.0** — HTML to Bricks 🧱
