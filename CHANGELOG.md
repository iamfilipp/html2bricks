# h2b Changelog

## Version 3.2.0 (2024-12-29)

### Critical Bug Fixes

**Property Naming Convention Fixed (BREAKING if you relied on wrong names):**
- ❌ OLD (WRONG): `_minHeight`, `_maxHeight`, `_minWidth`, `_maxWidth`
- ✅ NEW (CORRECT): `_heightMin`, `_heightMax`, `_widthMin`, `_widthMax`
- **Impact:** All sizing properties now output correctly to Bricks
- **Pattern:** `_[property][Min/Max]` NOT `_[min/max][Property]`
- **File Updated:** `references/BRICKS-NATIVE-PROPERTIES.md`

### New Guidance

**Classes and IDs:**
- Clarified `_cssClasses` is a space-separated STRING, not an array
- Example: `"_cssClasses": "class1 class2"` NOT `["class1", "class2"]`
- Documented that BOTH `_cssClasses` AND `_cssId` should be used
- `_cssClasses` → For reusable CSS selectors (`.my-class`)
- `_cssId` → For unique HTML IDs (`#my-element`)

**Custom CSS Property Removed:**
- Removed `_cssCustom` guidance - this property does NOT output to frontend
- All custom CSS must go in external CSS files
- Use ID or class selectors to target elements from external CSS

**Element Selection:**
- Added guidance on when to use `text` vs `heading` element
- Use `heading` for plain text only
- Use `text` element for rich HTML with styled `<span>` elements

### Version Updates

- Updated Bricks version from 1.12.4 to 2.1.4
- Updated skill version from 3.1.0 to 3.2.0

### Documentation Improvements

- Added section on zero dimensions causing collapse
- Clarified external CSS requirements
- Added more examples showing correct vs incorrect approaches
- Emphasized property naming pattern throughout

### Files Changed

1. `SKILL.md` - Version 3.2.0, added all new guidance
2. `references/BRICKS-NATIVE-PROPERTIES.md` - Fixed property names, added warnings
3. `CHANGELOG.md` - This file (NEW)

---

## Version 3.1.0 (Previous)

Initial version with flat structure, native property coverage, and comprehensive element support.
