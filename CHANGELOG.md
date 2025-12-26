# Changelog

All notable changes to h2b will be documented in this file.

## [3.1.1] - 2024-12-26

### Added
- Complete Grid system (10 properties): `_gridAutoColumns`, `_gridAutoRows`, `_gridAutoFlow`, `_justifyItemsGrid`, `_alignItemsGrid`, `_justifyContentGrid`, `_alignContentGrid`
- Complete Flexbox items (5 properties): `_flexGrow`, `_flexShrink`, `_flexBasis`, `_alignSelf`, `_order`
- Gap properties with units: `_columnGap`, `_rowGap` (accept string values with units like "30px")
- Tag property for all elements (not just headings): Override HTML tag output
- Display modes: `inline`, `inline-flex`, `inline-grid`

### Fixed
- BRICKS-ELEMENTS.md now documents tag property for structure elements
- BRICKS-NATIVE-PROPERTIES.md complete with all grid/flex properties
- Gap property documentation clarifies units vs numbers

### Documentation
- Updated examples with complete property usage
- Added tag property usage examples
- Clarified difference between `_gap` (number) and `_columnGap`/`_rowGap` (string with units)

---

## [3.1.0] - 2024-12-26

### Added - FLAT STRUCTURE (CRITICAL)
- **Flat structure with ID-based relationships** - All elements are siblings in content array
- Required fields on every element: `id`, `name`, `parent`, `children`, `settings`, `label`
- 31 Bricks elements reference (BRICKS-ELEMENTS.md)
- Pseudo-selector support for ALL properties (`:hover`, `:focus`, `:nth-child`, etc.)
- Native interactions system reference
- JavaScript handling strategy (4-tier system)

### Coverage
- 99.5%+ native property coverage
- External CSS only needed for `::before`, `::after`, complex selectors

### Breaking Changes
- Structure must be FLAT, not nested
- All elements require `id`, `parent`, `children` fields
- sourceUrl changed to: `https://github.com/iamfilipp/html2bricks`

---

## [3.0.0] - 2024-12

### Added
- Gradients support (`_gradient` object)
- Interactions system (`_interactions`)
- Advanced flexbox properties
- Advanced grid properties
- 25+ additional native properties

### Coverage
- 95% native property coverage

---

## [2.3.0] - Initial Release

### Added
- HTML to Bricks JSON conversion
- Basic CSS property mapping
- h2b- class prefix system
- ~60-70% property coverage
