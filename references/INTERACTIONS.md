# Interactions — Complete Reference

**Verified against Bricks 2.3.5 via live MCP**

Stored in `settings._interactions` as an array on any element.

**⚠️ NEVER use deprecated `_animation`, `_animationDuration`, `_animationDelay` keys.**

---

## Interaction Object Structure

```json
{
  "id": "aa1bb2",          // Required. Unique 6-char lowercase alphanumeric
  "trigger": "enterView",  // Required. See triggers list
  "action": "startAnimation", // Required. See actions list
  "target": "self",        // Optional: "self" (default), "custom", "popup"
  "targetSelector": "",    // Required when target="custom" (CSS selector)
  "templateId": 123,       // Required when target="popup"
  
  // Animation-specific
  "animationType": "fadeInUp",  // Required when action="startAnimation"
  "animationDuration": "0.8s",  // Optional (default "1s")
  "animationDelay": "0s",       // Optional (default "0s")
  "runOnce": true,              // Optional boolean
  
  // enterView-specific
  "rootMargin": "0px 0px -80px 0px",  // Optional IntersectionObserver margin
  
  // contentLoaded-specific
  "delay": "0.5s",              // Optional delay before firing
  
  // scroll-specific
  "scrollOffset": "300px",      // Scroll position (px/vh/%)
  
  // animationEnd-specific
  "animationId": "ii9jj0",      // ID of the interaction to wait for
  
  // javascript-specific
  "jsFunction": "myFn.parallax", // Global function name (no parentheses)
  "jsFunctionArgs": [{"id": "oo5pp6", "jsFunctionArg": "%brx%"}],
  
  // AJAX-specific
  "ajaxQueryId": "abc123",      // Required for ajaxStart/ajaxEnd
  
  // Form-specific
  "formId": "def456",           // Required for formSubmit/formSuccess/formError
  
  // Load more
  "loadMoreQuery": "main",                    // Required for loadMore
  "loadMoreTargetSelector": "#brxe-abc123",  // Required for loadMoreGallery
  
  // Conditional execution
  "interactionConditions": []   // Optional conditions array
}
```

---

## Triggers

| Trigger | When | Extra fields |
|---------|------|-------------|
| `click` | Element clicked | `disablePreventDefault` (bool) |
| `mouseover` | Mouse over element | |
| `mouseenter` | Mouse enters bounds | |
| `mouseleave` | Mouse leaves bounds | |
| `focus` | Element receives focus | |
| `blur` | Element loses focus | |
| `enterView` | Enters viewport | `rootMargin`, `runOnce` |
| `leaveView` | Leaves viewport | |
| `animationEnd` | Another animation ends | `animationId` (required) |
| `contentLoaded` | DOM ready | `delay` (optional, e.g. `"0.5s"`) |
| `scroll` | Window scroll | `scrollOffset` (px/vh/%) |
| `mouseleaveWindow` | Mouse leaves browser | |
| `ajaxStart` | Query loop AJAX starts | `ajaxQueryId` (required) |
| `ajaxEnd` | Query loop AJAX ends | `ajaxQueryId` (required) |
| `formSubmit` | Form submitted | `formId` (required) |
| `formSuccess` | Form succeeded | `formId` (required) |
| `formError` | Form failed | `formId` (required) |

---

## Actions

| Action | What it does | Extra fields |
|--------|-------------|-------------|
| `startAnimation` | Animate.css animation | `animationType`, `animationDuration`, `animationDelay` |
| `show` | Show element (remove display:none) | `target` |
| `hide` | Hide element (set display:none) | `target` |
| `click` | Programmatically click target | `target` |
| `setAttribute` | Set HTML attribute | `target`, attribute key/value |
| `removeAttribute` | Remove HTML attribute | `target` |
| `toggleAttribute` | Toggle HTML attribute | `target` |
| `toggleOffCanvas` | Toggle Bricks Offcanvas | `target` |
| `loadMore` | Load more in query loop | `loadMoreQuery` (usually `"main"`) |
| `loadMoreGallery` | Load more in Image Gallery (2.3+) | `loadMoreTargetSelector` |
| `scrollTo` | Smooth scroll to element | `target`, optional offset+delay |
| `javascript` | Call global JS function | `jsFunction`, `jsFunctionArgs` |
| `openAddress` | Open map info box | |
| `closeAddress` | Close map info box | |
| `clearForm` | Clear form fields | |
| `storageAdd` | Add to browser storage | |
| `storageRemove` | Remove from browser storage | |
| `storageCount` | Count browser storage items | |

---

## Animation Types (Animate.css)

Bricks auto-enqueues Animate.css. No manual enqueue needed.

**`*In` types auto-hide element on load and reveal on animation — use for entrances.**
**`*Out` types for exits or click-triggered hiding.**

### Attention
`bounce` `flash` `pulse` `rubberBand` `shakeX` `shakeY` `headShake` `swing` `tada` `wobble` `jello` `heartBeat`

### Back
`backInDown` `backInLeft` `backInRight` `backInUp` `backOutDown` `backOutLeft` `backOutRight` `backOutUp`

### Bounce
`bounceIn` `bounceInDown` `bounceInLeft` `bounceInRight` `bounceInUp`
`bounceOut` `bounceOutDown` `bounceOutLeft` `bounceOutRight` `bounceOutUp`

### Fade
`fadeIn` `fadeInDown` `fadeInDownBig` `fadeInLeft` `fadeInLeftBig` `fadeInRight` `fadeInRightBig` `fadeInUp` `fadeInUpBig` `fadeInTopLeft` `fadeInTopRight` `fadeInBottomLeft` `fadeInBottomRight`
`fadeOut` `fadeOutDown` `fadeOutDownBig` `fadeOutLeft` `fadeOutLeftBig` `fadeOutRight` `fadeOutRightBig` `fadeOutUp` `fadeOutUpBig` `fadeOutTopLeft` `fadeOutTopRight` `fadeOutBottomRight` `fadeOutBottomLeft`

### Flip
`flip` `flipInX` `flipInY` `flipOutX` `flipOutY`

### Light Speed
`lightSpeedInRight` `lightSpeedInLeft` `lightSpeedOutRight` `lightSpeedOutLeft`

### Rotate
`rotateIn` `rotateInDownLeft` `rotateInDownRight` `rotateInUpLeft` `rotateInUpRight`
`rotateOut` `rotateOutDownLeft` `rotateOutDownRight` `rotateOutUpLeft` `rotateOutUpRight`

### Special
`hinge` `jackInTheBox` `rollIn` `rollOut`

### Zoom
`zoomIn` `zoomInDown` `zoomInLeft` `zoomInRight` `zoomInUp`
`zoomOut` `zoomOutDown` `zoomOutLeft` `zoomOutRight` `zoomOutUp`

### Slide
`slideInUp` `slideInDown` `slideInLeft` `slideInRight`
`slideOutUp` `slideOutDown` `slideOutLeft` `slideOutRight`

---

## Patterns

### Scroll Reveal (most common entrance)
```json
"_interactions": [{
  "id": "aa1bb2",
  "trigger": "enterView",
  "rootMargin": "0px 0px -80px 0px",
  "action": "startAnimation",
  "animationType": "fadeInUp",
  "animationDuration": "0.8s",
  "animationDelay": "0s",
  "target": "self",
  "runOnce": true
}]
```

### Stagger Cards (apply each with incrementing delay)
```json
// Card 1
{"id": "cc3dd4", "trigger": "enterView", "action": "startAnimation", "animationType": "fadeInUp", "animationDuration": "0.8s", "animationDelay": "0s", "target": "self", "runOnce": true}
// Card 2
{"id": "ee5ff6", "trigger": "enterView", "action": "startAnimation", "animationType": "fadeInUp", "animationDuration": "0.8s", "animationDelay": "0.15s", "target": "self", "runOnce": true}
// Card 3
{"id": "gg7hh8", "trigger": "enterView", "action": "startAnimation", "animationType": "fadeInUp", "animationDuration": "0.8s", "animationDelay": "0.3s", "target": "self", "runOnce": true}
```

### Chained Animation (animationEnd trigger)
```json
// Title — fires on page load
{"id": "ii9jj0", "trigger": "contentLoaded", "action": "startAnimation", "animationType": "fadeInDown", "animationDuration": "0.8s", "target": "self"}

// Subtitle — fires when title animation ends
{"id": "kk1ll2", "trigger": "animationEnd", "animationId": "ii9jj0", "action": "startAnimation", "animationType": "fadeIn", "animationDuration": "0.6s", "target": "self"}
```

### Click Show/Hide
```json
// Show a target element on click
{"id": "pp1qq2", "trigger": "click", "action": "show", "target": "custom", "targetSelector": "#brxe-tooltip123"}

// Hide a target element on click
{"id": "pp3qq4", "trigger": "click", "action": "hide", "target": "custom", "targetSelector": "#brxe-tooltip123"}
```

### Popup Trigger
```json
{"id": "rr5ss6", "trigger": "click", "action": "show", "target": "popup", "templateId": 1234}
```

### Load More Button
```json
{"id": "tt7uu8", "trigger": "click", "action": "loadMore", "loadMoreQuery": "main"}
```

### Load More Gallery (Bricks 2.3+)
```json
{"id": "vv9ww0", "trigger": "click", "action": "loadMoreGallery", "loadMoreTargetSelector": "#brxe-galleryid"}
```

### GSAP via javascript action
```json
{
  "id": "mm3nn4",
  "trigger": "contentLoaded",
  "action": "javascript",
  "jsFunction": "brxGsap.parallax",
  "jsFunctionArgs": [{"id": "oo5pp6", "jsFunctionArg": "%brx%"}],
  "target": "self"
}
```
`%brx%` = Bricks params: `{source: sourceElement, targets: [], target: firstTarget}`

### Native Parallax (no interaction needed — use style properties)
```json
// Set directly on element settings — NOT in _interactions
{
  "_motionElementParallax": true,
  "_motionElementParallaxSpeedY": -20,
  "_motionStartVisiblePercent": 0
}
```

---

## Tips

- Default scroll entrance: `fadeInUp`, duration 0.8s
- Hero elements: `contentLoaded` trigger, no delay
- Below-fold elements: `enterView` trigger + `rootMargin "0px 0px -80px 0px"`
- Stagger increments: 0.1s–0.15s per element
- Max ~5–6 animated elements per viewport
- Every interaction `id` must be unique across the entire page
- `*In` animations hide the element on load automatically — correct for entrances
