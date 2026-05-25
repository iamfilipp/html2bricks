# h2b Changelog

## Version 4.0.0 (2025-05-25)

### MCP-Verified Rebuild — Bricks 2.3.5

This release was verified against a live Bricks 2.3.5 installation via MCP (Model Context Protocol) API, not documentation alone. Every property, element name, and schema field was confirmed from the live builder.

---

### Critical Corrections (previous versions were wrong)

**`_cssCustom` works — it was never broken.**
Previous versions stated `_cssCustom` "does NOT output to frontend CSS" and told users to use external files. This was incorrect. `_cssCustom` works correctly when the selector uses `#brxe-{elementId}` format:
```json
"_cssCustom": "#brxe-einrji { transform: rotate(45deg); mix-blend-mode: overlay; }"
```
The actual broken pattern was `%root%` — that does nothing via the API. All guidance updated accordingly.

**Gradient format corrected.**
v3.x documented gradients as a stops array. The actual format is a plain CSS string:
```json
// ✅ CORRECT
"_background": {"gradient": "linear-gradient(135deg, #667eea 0%, #764ba2 100%)"}

// ❌ OLD (WRONG) — stops array
"_background": {"gradient": {"type": "linear", "angle": "90", "stops": [...]}}
```

**`_textAlign` does nothing.**
`text-align` must go inside the `_typography` object:
```json
// ✅ CORRECT
"_typography": {"text-align": "center"}

// ❌ WRONG
"_textAlign": "center"
```

**`_gap` and `_display` don't apply to layout elements.**
`section`, `container`, `block`, `div` are always flex. `_gap` and `_display` have no effect on them. Use `_cssCustom` instead:
```json
"_cssCustom": "#brxe-abc123 { gap: 24px; }"
```

**`_animation` is deprecated (confirmed).**
The deprecated `_animation`, `_animationDuration`, `_animationDelay` keys were removed from guidance. Always use `_interactions` array. Bricks shows a converter warning for deprecated keys.

---

### New: Element Conditions Schema

Added `references/CONDITIONS.md` — complete `_conditions` reference verified from live API.

Structure:
```json
"_conditions": [
  [{"key": "user_logged_in", "compare": "==", "value": "1"}]
]
```
Outer array = OR logic, inner array = AND logic.

**All verified condition keys:**
- **Post:** `post_id`, `post_title`, `post_parent`, `post_status`, `post_author`, `post_date`, `featured_image`
- **User:** `user_logged_in`, `user_id`, `user_registered`, `user_role`
- **Date/Time:** `weekday`, `date`, `time`, `datetime`
- **Other:** `dynamic_data`, `browser`, `operating_system`, `current_url`, `referer`
- **WooCommerce:** `woo_product_type`, `woo_product_sale`, `woo_product_stock_status`, `woo_product_category`, `woo_product_purchased_by_user`, and more

---

### New: Native Parallax (Bricks 2.3+)

No JavaScript needed. Style properties set directly on elements:

```json
// Element parallax
{"_motionElementParallax": true, "_motionElementParallaxSpeedY": -20, "_motionStartVisiblePercent": 0}

// Background parallax
{"_motionBackgroundParallax": true, "_motionBackgroundParallaxSpeed": -15, "_motionStartVisiblePercent": 0}
```

---

### Updated: Full Interactions Schema

`references/INTERACTIONS.md` fully rewritten from live MCP API data:
- All 14 triggers with exact field names (`ajaxStart`, `ajaxEnd`, `formSubmit`, `formSuccess`, `formError` added)
- All 17 actions including `loadMoreGallery` (new in Bricks 2.3+)
- Exact interaction object fields: `id`, `trigger`, `action`, `target`, `targetSelector`, `templateId`, `animationType`, `animationDuration`, `animationDelay`, `rootMargin`, `runOnce`, `delay`, `scrollOffset`, `animationId`, `jsFunction`, `jsFunctionArgs`
- Full Animate.css type list (attention, back, bounce, fade, flip, lightspeed, rotate, special, zoom, slide)
- 7 copy-paste patterns: scroll reveal, stagger cards, chained animation, click show/hide, popup trigger, load more, GSAP bridge

---

### Expanded: 166+ Elements

`references/BRICKS-ELEMENTS.md` expanded from 31 to 166+ elements across all categories. Correct `name` slugs verified from live API:
- Layout (4), Basic (8), General (30), Media (7), Query (2)
- Single Post (13), WordPress (6), Filter (8)
- WooCommerce Store/Cart/Checkout/Account (24+), WooCommerce Product (14+)

---

### Version Updates

- Bricks version: `2.1.4` → `2.3.5`
- Skill version: `3.2.0` → `4.0.0`
- mobian.eu → mobians.co (domain update)

---

### Files Changed

| File | Change |
|------|--------|
| `SKILL.md` | Rewritten — corrected `_cssCustom`, gotchas, native parallax, v4.0.0 |
| `references/BRICKS-ELEMENTS.md` | Expanded 31 → 166+ elements |
| `references/BRICKS-NATIVE-PROPERTIES.md` | Fixed gradients, `_textAlign`, `_gap` on layout elements, added parallax properties |
| `references/INTERACTIONS.md` | Full rewrite — all triggers/actions/fields from live API |
| `references/CONDITIONS.md` | **NEW** — complete element conditions schema |
| `references/JAVASCRIPT-HANDLING.md` | No change |
| `references/PSEUDO-SELECTORS.md` | No change |
| `h2b.skill` | Repackaged with all above |

---

## Version 3.2.0 (2024-12-29)

### Critical Bug Fixes

**Property Naming Convention Fixed:**
- ❌ OLD: `_minHeight`, `_maxHeight`, `_minWidth`, `_maxWidth`
- ✅ NEW: `_heightMin`, `_heightMax`, `_widthMin`, `_widthMax`

### New Guidance

- `_cssClasses` is a space-separated STRING, not an array
- Both `_cssClasses` AND `_cssId` should be used together
- `_cssCustom` removed (use external CSS files) ← *corrected in v4.0.0*
- Added `text` vs `heading` element selection guidance

### Version Updates

- Bricks version: `1.12.4` → `2.1.4`
- Skill version: `3.1.0` → `3.2.0`

---

## Version 3.1.0

Initial release with flat structure, native property coverage, and element support.
