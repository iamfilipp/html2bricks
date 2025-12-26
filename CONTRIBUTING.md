# Contributing to h2b

Thank you for considering contributing to h2b!

## How to Contribute

### Reporting Bugs

1. **Check existing issues** - See if the bug has been reported
2. **Create detailed report** - Include:
   - Input HTML/CSS
   - Expected Bricks JSON output
   - Actual output
   - h2b version
   - Error messages

### Suggesting Features

1. **Check existing feature requests**
2. **Open issue** with:
   - Use case description
   - Example input/output
   - Why it would be valuable

### Submitting Examples

We welcome new working examples!

**Requirements:**
- Must use flat structure (ID-based relationships)
- All required fields present (id, name, parent, children, settings, label)
- 99.5%+ native properties
- Test in Bricks Builder
- Include README.md with features demonstrated

**Example structure:**
```
examples/04-new-example/
├── component-name.json
└── README.md
```

### Improving Documentation

- Fix typos or unclear explanations
- Add examples to reference guides
- Improve SKILL.md clarity

### Code Style

**JSON formatting:**
- 2-space indentation
- Flat structure (no nested children objects)
- Required fields order: id, name, parent, children, settings, label

**Bricks JSON requirements:**
```json
{
  "id": "unique-id",
  "name": "element-type",
  "parent": 0,
  "children": [],
  "settings": {},
  "label": "Display Name"
}
```

## Pull Request Process

1. **Fork the repository**
2. **Create feature branch** - `git checkout -b feature/new-example`
3. **Make changes** following style guidelines
4. **Test in Bricks Builder** - Ensure JSON works
5. **Commit** with clear message
6. **Push** to your fork
7. **Open Pull Request** with:
   - Description of changes
   - Why it's needed
   - Screenshots/examples if applicable

## Testing

Before submitting:
1. ✅ JSON is valid
2. ✅ Flat structure used
3. ✅ All required fields present
4. ✅ Paste works in Bricks Builder
5. ✅ No console errors

## Questions?

Open an issue or reach out to [@iamfilipp](https://github.com/iamfilipp)

---

Thank you for contributing! 🎉
