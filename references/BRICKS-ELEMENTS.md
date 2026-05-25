# Bricks Builder Elements Reference

**Total elements: 166+ (Bricks 2.3.5)**

## Layout Elements (4)

| Name | Label | HTML mapping |
|------|-------|-------------|
| `section` | Section | `<section>`, `<header>`, `<main>`, `<footer>`, `<article>` |
| `container` | Container | `<div class="container">` (max-width, centered) |
| `block` | Block | `<div>` for flex/grid layout columns/rows |
| `div` | Div | `<div>` generic wrapper |

**Decision rule:**
- `section` → root level page regions (100% wide, flex)
- `container` → centered max-width content wrapper (1100px default)
- `block` → flex columns/rows inside container (100% wide)
- `div` → decorative/absolute positioned / unstyled wrapper

---

## Basic Elements (8)

| Name | Label | Settings | HTML mapping |
|------|-------|---------|-------------|
| `heading` | Heading | `{text, tag}` — tag: h1–h6 | `<h1>`–`<h6>` |
| `text-basic` | Basic Text | `{text}` | `<p>` |
| `text` | Rich Text | `{text}` — accepts HTML markup | `<div>` with HTML |
| `text-link` | Text link | `{text, link: {type, url}}` | `<a>` |
| `button` | Button | `{text, style, link}` | `<button>`, `<a class="btn">` |
| `icon` | Icon | `{icon: {library, icon}}` | `<i>`, `<svg>`, icon fonts |
| `image` | Image | `{image: {url, external, filename}}` | `<img>` |
| `video` | Video | `{videoType, videoUrl}` or `{videoType: "media", video: {id, url}}` | `<video>`, YouTube/Vimeo `<iframe>` |

**Icon libraries:** `Ionicons`, `FontAwesome`, `Themify`

**Heading tag setting:**
```json
{"text": "My Heading", "tag": "h1"}
```

**Button with link:**
```json
{"text": "Click me", "link": {"type": "external", "url": "https://..."}}
```

**Video types:** `youtube`, `vimeo`, `media` (self-hosted), `file`, `meta`
Self-hosted video (Bricks 2.3+) supports `objectFit: "cover"`.

---

## General Elements (30)

| Name | Label | Key settings |
|------|-------|-------------|
| `accordion` | Accordion | `{accordions: [{title, content}]}` |
| `accordion-nested` | Accordion (Nestable) | Nested block structure |
| `alert` | Alert | `{title, content, type}` |
| `animated-typing` | Anim. Typing | `{strings: [], typeSpeed, backSpeed}` |
| `back-to-top` | Back to Top | Nested icon + text structure |
| `breadcrumbs` | Breadcrumbs | No required settings |
| `code` | Code | `{code}` — PHP/HTML execution |
| `countdown` | Countdown | `{date: "2026-01-01 12:00"}` |
| `counter` | Counter | `{countTo: 1000, prefix, suffix, duration}` |
| `divider` | Divider | No required settings |
| `dropdown` | Dropdown | Nested trigger + content |
| `facebook-page` | Facebook Page | `{pageUrl}` |
| `form` | Form | `{fields: [], actions: []}` |
| `html` | HTML | `{code}` — raw HTML |
| `icon-box` | Icon Box | `{icon, title, text}` |
| `list` | List | `{items: [], tag}` |
| `logo` | Logo | `{image, link}` |
| `map` | Map (Google) | `{addresses: [{latitude, longitude}]}` |
| `map-connector` | Map Connector | Advanced map filtering |
| `map-leaflet` | Map (Leaflet) | `{addresses}` — no API key |
| `nav-nested` | Nav (Nestable) | Nested block structure |
| `offcanvas` | Offcanvas | `{position}` — left/right/top/bottom |
| `pie-chart` | Pie Chart | `{percent: 60}` |
| `pricing-tables` | Pricing Tables | `{pricingTables: [{name, price, features}]}` |
| `progress-bar` | Progress Bar | `{value: 75, label}` |
| `rating` | Rating | `{rating: 4, maxRating: 5}` |
| `slot` | Slot | Component content injection point |
| `social-icons` | Icon List | `{items: [{icon, link}]}` |
| `tabs` | Tabs | `{tabs: [{title, content}]}` |
| `tabs-nested` | Tabs (Nestable) | Nested block structure |
| `team-members` | Team Members | `{items: [{name, role, image}]}` |
| `template` | Template | `{templateId: 123}` |
| `testimonials` | Testimonials | `{items: [{content, name}]}` |
| `toggle` | Toggle | Targets offcanvas or CSS selector |
| `toggle-mode` | Toggle - Mode | `{ariaLabel}` — dark/light toggle |

---

## Media Elements (7)

| Name | Label | Notes |
|------|-------|-------|
| `audio` | Audio | `{audio: {url}}` |
| `carousel` | Carousel | `{fields: [{image, title, content}]}` |
| `image-gallery` | Image Gallery | `{items: {images: [...]}}` |
| `instagram-feed` | Instagram feed | Requires access token |
| `slider` | Slider | `{items: [{title, content}]}` |
| `slider-nested` | Slider (Nestable) | Nested slide blocks |
| `svg` | SVG | Inline SVG display |

**Image Gallery Load More (Bricks 2.3+):**
```json
{
  "loadMoreInitial": 6,
  "loadMoreStep": 3,
  "loadMoreInfiniteScroll": true,
  "loadMoreInfiniteScrollDelay": "600ms",
  "loadMoreInfiniteScrollOffset": "200px"
}
```

---

## Query Elements (2)

| Name | Label | Notes |
|------|-------|-------|
| `pagination` | Pagination | Link to query loop via `relatedQueryId` |
| `query-results-summary` | Query Results Summary | Shows "X–Y of Z results" |

---

## Single Post Elements (13)

| Name | Label |
|------|-------|
| `post-author` | Author |
| `post-comments` | Comments |
| `post-content` | Post Content |
| `post-excerpt` | Excerpt |
| `post-meta` | Meta Data |
| `post-navigation` | Post Navigation |
| `post-reading-progress-bar` | Reading progress bar |
| `post-reading-time` | Reading time |
| `post-sharing` | Social Sharing |
| `post-taxonomy` | Taxonomy |
| `post-title` | Post Title |
| `post-toc` | Table of contents |
| `related-posts` | Related Posts |

---

## WordPress Elements (6)

| Name | Label |
|------|-------|
| `nav-menu` | Nav Menu |
| `posts` | Posts |
| `search` | Search |
| `shortcode` | Shortcode — `{shortcode: "[my_shortcode]"}` |
| `sidebar` | Sidebar |
| `wordpress` | WordPress widget |

---

## Filter Elements (8) — Query Sort/Filter feature

| Name | Label |
|------|-------|
| `filter-active-filters` | Active Filters |
| `filter-checkbox` | Filter Checkbox |
| `filter-datepicker` | Filter Datepicker |
| `filter-radio` | Filter Radio |
| `filter-range` | Filter Range |
| `filter-search` | Filter Search |
| `filter-select` | Filter Select |
| `filter-submit` | Filter Submit |

---

## WooCommerce Elements (24)

**Store:**
`woocommerce-products` · `woocommerce-products-filter` · `woocommerce-products-orderby` · `woocommerce-products-pagination` · `woocommerce-products-total-results` · `woocommerce-products-archive-description` · `woocommerce-mini-cart` · `woocommerce-breadcrumbs` · `woocommerce-notice`

**Cart:**
`woocommerce-cart-items` · `woocommerce-cart-coupon` · `woocommerce-cart-collaterals`

**Checkout:**
`woocommerce-checkout-customer-details` · `woocommerce-checkout-order-payment` · `woocommerce-checkout-order-review` · `woocommerce-checkout-order-table` · `woocommerce-checkout-thankyou`

**Account (13):**
`woocommerce-account-page` · `woocommerce-account-form-login` · `woocommerce-account-form-register` · `woocommerce-account-form-edit-account` · `woocommerce-account-addresses` · `woocommerce-account-form-edit-address` · `woocommerce-account-orders` · `woocommerce-account-view-order` · `woocommerce-account-downloads` · `woocommerce-account-payment-methods` · `woocommerce-account-add-payment-method` · `woocommerce-account-form-lost-password` · `woocommerce-account-form-reset-password`

---

## WooCommerce Product Elements (15)

| Name | Label |
|------|-------|
| `product-title` | Product title |
| `product-price` | Product price |
| `product-rating` | Product rating |
| `product-gallery` | Product gallery |
| `product-short-description` | Product short description |
| `product-content` | Product content |
| `product-meta` | Product meta |
| `product-stock` | Product stock |
| `product-tabs` | Product tabs |
| `product-reviews` | Product reviews |
| `product-additional-information` | Product additional information |
| `product-add-to-cart` | Add to cart |
| `product-related` | Related products |
| `product-upsells` | Product up/cross-sells |

---

## HTML to Bricks Element Mapping

```
HTML Tag              → Bricks Element
─────────────────────────────────────────────
<section>             → section
<header>              → section
<main>                → section
<footer>              → section
<article>             → section (or block)
<div class="container"> → container
<div> (flex layout)   → block
<div> (wrapper)       → div
<h1>–<h6>             → heading (with tag: "h1"–"h6")
<p>                   → text-basic
<div> with HTML       → text (rich text)
<a>                   → text-link
<button>              → button
<a class="btn">       → button
<img>                 → image
<video>               → video
<audio>               → audio
<svg>                 → svg
<hr>                  → divider
<ul>/<ol> with icons  → social-icons (icon-list)
<nav>                 → nav-nested or nav-menu
```

---

## Context-Based Element Selection

**`div` vs `block` vs `container` vs `section`:**
- Root page region (full width, different bg) → `section`
- Centered content area (max-width) → `container`
- Flex column/row inside container → `block`
- Decorative/absolute/unstyled → `div`

**`text` vs `text-basic` vs `heading`:**
- `heading` — plain text only, semantic h1–h6
- `text-basic` — simple `<p>` paragraph
- `text` — any rich HTML (`<span>`, `<strong>`, `<em>`, custom classes inside)
