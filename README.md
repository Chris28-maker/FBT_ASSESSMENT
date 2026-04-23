# FBT_ASSESSMENT
Trade-offs & Known Limitations
⚠️ Variant selection not implemented
Currently uses selected_or_first_available_variant for complementary products. For products with multiple variants, the customer cannot choose a specific size/colour before adding. The clean architectural fix is to render a <select> per complementary product and update the checkbox value on change.
⚠️ No quantity input
Each item is added with quantity: 1. A production implementation might include a stepper, but it's outside scope for this assessment.
CSS Architecture
Uses CSS Custom Properties scoped to .fbt-section. Merchants can override the palette:
css.fbt-section {
  --fbt-accent: #2c5f2e;
  --fbt-check:  #2c5f2e;
}
Responsive Breakpoints:

≥ 901px: horizontal row of cards + CTA on the right
641px–900px: tablet layout, cards wrap, CTA below
≤ 640px: vertical stack, horizontal card layout (image left, text right)

Respects prefers-reduced-motion.
Cart Integration
Uses Dawn's section rendering API (/?sections=cart-icon-bubble) to update the cart bubble count without page reload.
Accessibility

<section aria-labelledby> with visible heading
Each card is a <label> wrapping <input type="checkbox"> — keyboard navigable
aria-live="polite" on price total and feedback
All images have meaningful alt attributes
Sold-out overlay and + connectors are aria-hidden

Browser Support
Chrome 80+, Firefox 75+, Safari 13+, Edge 80+. No polyfills needed.
