# RankAPI Audit Request Modal — Design Spec

**Date:** 2026-04-25
**Status:** Approved

## Overview

Replace the Google Form (bit.ly link) with an embedded modal form on the landing page. The modal contains a 6-field form that submits to Formspree.

---

## Modal

**Trigger:** Both CTA buttons ("Reserve your free audit →" and "Join the waitlist →") open the modal instead of linking to bit.ly.

**Backdrop:** `rgba(8,11,16,0.85)` with `backdrop-filter: blur(4px)`. Clicking backdrop closes modal.

**Animation:** Fade in + scale from 0.95 to 1.0, 200ms ease-out.

**Close:** X button top-right corner of modal box.

---

## Form Fields (6 total)

| # | Field | Type | Required |
|---|-------|------|----------|
| 1 | Name | text | yes |
| 2 | Email address | email | yes |
| 3 | API Name | text | yes |
| 4 | API Website | url | yes |
| 5 | Primary goal | dropdown | yes |
| 6 | How did you hear about us? | dropdown | no |

**Dropdown options — Primary goal:**
- Increase visibility
- Benchmark competitors
- Improve positioning

**Dropdown options — How did you hear about us?**
- Google
- AI recommendation
- Twitter / X
- LinkedIn
- Word of mouth
- Other

---

## Visual Style

- Modal box: `background: #0d1117`, border `1px solid #1e2d3d`, border-radius `10px`, max-width `480px`, centered
- Form header: "Get your free audit" (Syne, bold) + subtitle "Is your API invisible in AI chat responses? Get your free visibility audit."
- Inputs: `background: #111820`, border `1px solid #1e2d3d`, `border-radius: 4px`, `color: #e2e8f0`, font `DM Mono`
- Labels: uppercase, small, muted color, `DM Mono`
- Submit button: full width, `#4B8BF5` background, white text, same style as `.btn-primary`
- Focus state: blue border glow `rgba(29,78,216,0.5)`

---

## States

**Default:** Form displayed with all 6 fields + submit button.

**Success:** Form replaced with green checkmark icon + "Thanks! We'll be in touch." message + close button.

**Error:** Inline red message below submit button: "Something went wrong. Please try again."

---

## Formspree Integration

- `action="https://formspree.io/f/xbdqbyzb"`
- `method="POST"`
- `Accept: application/json` header for JSON response handling
- JavaScript intercepts submit, sends via fetch, handles success/error states inline (no page redirect)

---

## Implementation Steps

1. Add modal HTML structure (hidden by default)
2. Add modal CSS styles (backdrop, box, animation, inputs, button)
3. Add modal JS (open/close handlers, form submit interceptor with fetch)
4. Update both CTA buttons to open modal via onclick
5. Test Formspree submission end-to-end

---

## Files Modified

- `index.html` — add modal markup, CSS, JS inline