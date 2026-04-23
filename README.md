# Frequently Bought Together — Shopify OS 2.0 - DAWN

A lightweight, custom-built "Frequently Bought Together" section for Shopify Online Store 2.0 themes. No third-party apps, no jQuery.

---

## How It Works

### Data Layer — Metafields
| Property | Value |
|---|---|
| **Namespace** | `custom` |
| **Key** | `complementary_products` |
| **Type** | `list.product_reference` |
| **Max entries** | 2 |

### Setup
1. **Settings → Custom data → Products → Add definition**
   - Namespace/key: `custom.complementary_products`
   - Type: List of products
2. Upload `frequently-bought-together.liquid` to your theme's `sections/` folder
3. Add the section to your product template via **Online Store → Themes → Customize**
4. Open any product → scroll to Metafields → assign 1–2 complementary products → Save

---

## Architectural Decisions

- **Single-file section** — All Liquid, CSS, and JS in one file using `{% stylesheet %}` and `{% javascript %}` tags. Shopify deduplicates and minifies automatically.
- **Metafield-based data** — Manual curation gives merchandising team full editorial control.
- **Single AJAX request** — `/cart/add.js` accepts an `items` array, adding all variants in one request.
- **No jQuery** — Pure ES6+ using `fetch`, `classList`, `querySelectorAll`, and custom events.
- **Cart bubble update** — Uses Dawn's section rendering API (`/?sections=cart-icon-bubble`) to update cart count without page reload.

---

## Trade-offs & Limitations

⚠️ **Variant selection not implemented**
Currently uses `selected_or_first_available_variant` for complementary products. The fix is to render a `<select>` per complementary product and update the checkbox `value` on change.

⚠️ **No quantity input**
Each item is added with `quantity: 1`. Outside scope for this assessment.

---

## CSS Architecture

Uses CSS Custom Properties scoped to `.fbt-section`:

```css
.fbt-section {
  --fbt-accent: #2c5f2e;
  --fbt-check:  #2c5f2e;
}
```

**Responsive Breakpoints:**
- ≥ 901px: horizontal row of cards + CTA on the right
- 641px–900px: tablet layout, cards wrap, CTA below
- ≤ 640px: vertical stack, horizontal card layout

Respects `prefers-reduced-motion`.

---

## Accessibility

- `<section aria-labelledby>` with visible heading
- Each card is a `<label>` wrapping `<input type="checkbox">` — keyboard navigable
- `aria-live="polite"` on price total and feedback
- All images have meaningful `alt` attributes
- Sold-out overlay and `+` connectors are `aria-hidden`

---

## Browser Support

Chrome 80+, Firefox 75+, Safari 13+, Edge 80+. No polyfills needed.
