# Element Conditions — Complete Reference

**Verified against Bricks 2.3.5 via live MCP**

Stored in `settings._conditions` — controls whether an element renders on the frontend.
Evaluated server-side at render time.

**Note:** Element conditions are DIFFERENT from template conditions (which control which pages a template appears on).

---

## Data Structure

```json
"_conditions": [
  [{"key": "...", "compare": "...", "value": "..."}],   // Set 1
  [{"key": "...", "compare": "...", "value": "..."}]    // Set 2
]
```

- **Outer array** = OR logic (any set passing = element renders)
- **Inner array** = AND logic (all conditions in a set must pass)

---

## Condition Keys by Group

### Post Group

| Key | Description | Compare operators | Value type |
|-----|-------------|-------------------|-----------|
| `post_id` | Current post ID | `==` `!=` `>=` `<=` `>` `<` | string (numeric) |
| `post_title` | Post title | `==` `!=` `contains` `contains_not` | string |
| `post_parent` | Parent post ID | `==` `!=` `>=` `<=` `>` `<` | string (numeric, default 0) |
| `post_status` | Post status | `==` `!=` | array (e.g. `["publish","draft"]`) |
| `post_author` | Post author user ID | `==` `!=` | string (user ID) |
| `post_date` | Publish date | `==` `!=` `>=` `<=` `>` `<` | string (Y-m-d) |
| `featured_image` | Has featured image | `==` `!=` | string ("1" = set, "0" = not) |

### User Group

| Key | Description | Compare operators | Value type |
|-----|-------------|-------------------|-----------|
| `user_logged_in` | Login status | `==` `!=` | string ("1" = logged in, "0" = logged out) |
| `user_id` | Current user ID | `==` `!=` `>=` `<=` `>` `<` | string (numeric) |
| `user_registered` | Registration date | `<` `>` | string (Y-m-d) |
| `user_role` | User role | `==` `!=` | array (role slugs) |

### Date & Time Group

| Key | Description | Compare operators | Value type |
|-----|-------------|-------------------|-----------|
| `weekday` | Day of week | `==` `!=` `>=` `<=` `>` `<` | string (1–7, Monday=1, Sunday=7) |
| `date` | Current date (WP timezone) | `==` `!=` `>=` `<=` `>` `<` | string (Y-m-d) |
| `time` | Current time (WP timezone) | `==` `!=` `>=` `<=` `>` `<` | string (H:i, e.g. "09:00") |
| `datetime` | Date and time combined | `==` `!=` `>=` `<=` `>` `<` | string (Y-m-d h:i a) |

### Other Group

| Key | Description | Compare operators | Value type |
|-----|-------------|-------------------|-----------|
| `dynamic_data` | Any dynamic data tag | `==` `!=` `>=` `<=` `>` `<` `contains` `contains_not` `empty` `empty_not` | string; set tag in `dynamic_data` field |
| `browser` | Browser detection | `==` `!=` | string (chrome, firefox, safari, edge, opera, msie) |
| `operating_system` | OS detection | `==` `!=` | string (windows, mac, linux, ubuntu, iphone, ipad, ipod, android) |
| `current_url` | Current page URL | `==` `!=` `contains` `contains_not` | string |
| `referer` | HTTP referrer URL | `==` `!=` `contains` `contains_not` | string |

### WooCommerce Group (requires WooCommerce active)

| Key | Description | Value type |
|-----|-------------|-----------|
| `woo_product_type` | Product type | string (simple, grouped, external, variable) |
| `woo_product_sale` | On sale | string ("1" / "0") |
| `woo_product_new` | Is new | string ("1" / "0") |
| `woo_product_stock_status` | Stock status | string (instock, outofstock, onbackorder) |
| `woo_product_stock_quantity` | Stock quantity | string (numeric) |
| `woo_product_featured` | Is featured | string ("1" / "0") |
| `woo_product_purchased_by_user` | Purchased by user | string ("1" / "0") |
| `woo_product_rating` | Average rating | string (numeric) |
| `woo_product_category` | Product category | array (term IDs) |
| `woo_product_tag` | Product tag | array (term IDs) |

---

## Examples

### Logged-in users only
```json
"_conditions": [
  [{"key": "user_logged_in", "compare": "==", "value": "1"}]
]
```

### Admin or Editor role
```json
"_conditions": [
  [{"key": "user_role", "compare": "==", "value": ["administrator", "editor"]}]
]
```

### Business hours (Monday–Friday, 9am–5pm)
```json
"_conditions": [
  [
    {"key": "weekday", "compare": ">=", "value": "1"},
    {"key": "weekday", "compare": "<=", "value": "5"},
    {"key": "time", "compare": ">=", "value": "09:00"},
    {"key": "time", "compare": "<=", "value": "17:00"}
  ]
]
```

### Date-limited banner (before a specific date)
```json
"_conditions": [
  [{"key": "date", "compare": "<", "value": "2025-12-31"}]
]
```

### ACF field value (dynamic data condition)
```json
"_conditions": [
  [
    {
      "key": "dynamic_data",
      "compare": "==",
      "value": "1",
      "dynamic_data": "{acf_show_banner}"
    }
  ]
]
```

### Admin OR post has featured image (OR logic = two sets)
```json
"_conditions": [
  [{"key": "user_role", "compare": "==", "value": ["administrator"]}],
  [{"key": "featured_image", "compare": "==", "value": "1"}]
]
```

### WooCommerce sale badge (on sale only)
```json
"_conditions": [
  [{"key": "woo_product_sale", "compare": "==", "value": "1"}]
]
```

### Hide on mobile (OS check)
```json
"_conditions": [
  [
    {"key": "operating_system", "compare": "!=", "value": "iphone"},
    {"key": "operating_system", "compare": "!=", "value": "android"}
  ]
]
```

---

## Compare Operators Reference

| Operator | Meaning |
|----------|---------|
| `==` | Equal |
| `!=` | Not equal |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal |
| `<=` | Less than or equal |
| `contains` | String contains |
| `contains_not` | String does not contain |
| `empty` | Value is empty |
| `empty_not` | Value is not empty |
