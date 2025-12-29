# h2b - HTML to Bricks Builder Converter

(Claude AI Skill)

**Version 3.2.0** | 99.5%+ Native Coverage | Flat Structure Architecture

Convert HTML, CSS, and JavaScript to Bricks Builder paste-ready JSON format with complete property support and native interactions.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 🎯 What's New in v3.2.0

**Critical Fixes:**
- ✅ **Property Names Corrected** - `_heightMin`/`_widthMax` (not `_minHeight`/`_maxWidth`)
- ✅ **Classes Format Clarified** - `_cssClasses` is a space-separated string, not array
- ✅ **Both IDs Required** - Use `_cssClasses` AND `_cssId` together
- ✅ **Custom CSS Guidance** - `_cssCustom` removed (use external CSS files)
- ✅ **Element Selection** - Added `text` vs `heading` guidance for rich HTML
- ✅ **Bricks Updated** - Now targets Bricks Builder 2.1.4

See [CHANGELOG.md](CHANGELOG.md) for details.

---

## 🚀 Key Features

- ✅ **Flat Structure** - ID-based parent/children relationships
- ✅ **31 Bricks Elements** - Complete element library
- ✅ **Pseudo-Selectors** - Native `:hover`, `:focus`, `:nth-child`
- ✅ **Native Interactions** - JavaScript → `_interactions`
- ✅ **99.5%+ Coverage** - All major CSS properties
- ✅ **Complete Grid** - Auto-flow, alignment, spanning
- ✅ **Complete Flexbox** - Grow, shrink, basis, order

---

## 📦 Quick Start

### For Claude AI

1. Download `h2b.skill`
2. Claude.ai → Settings → Skills → Upload
3. Prompt: "Convert this HTML to Bricks JSON"

### Manual

Copy JSON from `examples/` into Bricks Builder.

---

## 📚 Examples

- **[01-simple-hero](examples/01-simple-hero/)** - Fullscreen hero with hover effects

---

## 🏗️ Flat Structure

```json
{
  "content": [
    {"id": "parent", "parent": 0, "children": ["child1"]},
    {"id": "child1", "parent": "parent", "children": []}
  ]
}
```

**Required fields:** `id`, `name`, `parent`, `children`, `settings`, `label`

**Critical:** Both `_cssClasses` (string) and `_cssId` should be added to elements:

```json
{
  "settings": {
    "_cssClasses": "my-class another-class",
    "_cssId": "unique-id"
  }
}
```

---

## 🎨 Coverage: 99.5%+

✅ Layout, Flexbox, Grid, Typography, Background, Border, Effects, Pseudo-selectors, Interactions

❌ Only `::before`, `::after`, complex selectors, `mix-blend-mode`, `@keyframes` need external CSS

---

## 🔧 Property Naming Pattern

**Correct Pattern:** `_[property][Min/Max]`

```json
"_widthMin": "320"    ✅ CORRECT
"_widthMax": "1200"   ✅ CORRECT
"_heightMin": "100vh" ✅ CORRECT
"_heightMax": "800"   ✅ CORRECT

"_minWidth": "320"    ❌ WRONG
"_maxWidth": "1200"   ❌ WRONG
```

---

## 📖 Documentation

Skill includes 5 reference guides:
1. **BRICKS-ELEMENTS.md** - Complete element library
2. **BRICKS-NATIVE-PROPERTIES.md** - All native properties (updated v3.2.0)
3. **PSEUDO-SELECTORS.md** - Pseudo-selector conversion
4. **INTERACTIONS.md** - Native interactions system
5. **JAVASCRIPT-HANDLING.md** - JavaScript processing

---

## 🐛 Known Limitations

- `_cssCustom` property doesn't output to frontend (use external CSS)
- Complex transforms need external CSS: `rotate() + translateY()`
- Zero width/height causes collapse for positioned children

---

## 👤 Author

**Filipp Gavrilos** / Mobian Agency  
GitHub: [@iamfilipp](https://github.com/iamfilipp) | [mobian.eu](https://mobian.eu)

---

## 📄 License

MIT - see [LICENSE](LICENSE)

---

**h2b v3.2.0** - Transforming HTML to Bricks 🧱
