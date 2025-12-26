# Example 1: Simple Hero Section

Fullscreen hero section with title, subtitle, and CTA button with hover effects.

## Features

- ✅ Flat structure with 5 elements
- ✅ Flexbox vertical/horizontal centering
- ✅ Typography properties
- ✅ Button hover effects (background, transform, shadow)
- ✅ Smooth transitions

## Structure

```
hero-section (section) - Full viewport height, flex center
└── hero-container (container) - Max-width 800px, flex column
    ├── hero-title (heading h1) - 56px white text
    ├── hero-subtitle (text-basic) - 20px gray text
    └── hero-cta (button) - Blue button with hover lift
```

## How to Use

1. Open Bricks Builder
2. Copy entire contents of `hero-section.json`
3. Structure Panel → Paste (Ctrl+V / Cmd+V)
4. Customize text, colors, spacing

## Properties Demonstrated

- `_height: "100vh"` - Full viewport
- `_display: "flex"` + `_alignItems` + `_justifyContent` - Centering
- `_background:hover` - Hover color change
- `_transform:hover` - Lift effect (-2px translateY)
- `_boxShadow:hover` - Shadow on hover
- `_cssTransition` - Smooth animations

## Visual

**Dark background (#1a1a2e)**  
**White heading (56px)**  
**Gray subtitle (20px)**  
**Blue CTA (#0066cc) → Darker on hover (#0052a3)**
