# h2b - HTML to Bricks Builder Converter

**Version 3.1.1** | 99.5%+ Native Coverage | Flat Structure Architecture

Convert HTML, CSS, and JavaScript to Bricks Builder paste-ready JSON format with complete property support and native interactions.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

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

---

## 🎨 Coverage: 99.5%+

✅ Layout, Flexbox, Grid, Typography, Background, Border, Effects, Pseudo-selectors, Interactions

❌ Only `::before`, `::after`, complex selectors need external CSS

---

## 📖 Documentation

Skill includes 5 reference guides:
1. BRICKS-ELEMENTS.md
2. BRICKS-NATIVE-PROPERTIES.md  
3. PSEUDO-SELECTORS.md
4. INTERACTIONS.md
5. JAVASCRIPT-HANDLING.md

---

## 👤 Author

**Filipp Gavrilos** / Mobian Agency  
GitHub: [@iamfilipp](https://github.com/iamfilipp) | [mobian.eu](https://mobian.eu)

---

## 📄 License

MIT - see [LICENSE](LICENSE)

---

**h2b v3.1.1** - Transforming HTML to Bricks 🧱
