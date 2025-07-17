---
title: web-buttons
type: note
permalink: design-guidelines/web-buttons
---

# Web Buttons

## Button System

We have implemented a global button system with three main button styles. Here's how to use them:

### Button Classes Overview

| User Request            | CSS Class               | Appearance                                    | Usage                                       |
| ----------------------- | ----------------------- | --------------------------------------------- | ------------------------------------------- |
| "Primary Button"        | `primary-button`        | White background, red text, red border        | Main actions, call-to-action buttons        |
| "Secondary Button"      | `secondary-button`      | Light grey background, dark text, grey border | Less prominent actions, alternative options |
| "Primary Button Strong" | `primary-button-strong` | Red background, white text, red border        | High-emphasis actions, navigation CTAs      |

### Implementation

To apply these styles, add the appropriate class to any `b-button` component:

```vue
<!-- Primary Button (Red text on white) -->
<b-button class="primary-button">
  Download App
</b-button>

<!-- Secondary Button (Grey background) -->
<b-button class="secondary-button">
  Frequently Asked Questions
</b-button>

<!-- Primary Strong Button (White text on red) -->
<b-button class="primary-button-strong">
  Sign-up
</b-button>
```

### CSS Definitions

Located in `/src/assets/scss/helpers.scss`:

```scss
// PRIMARY BUTTON (Red text on white background)
.button.primary-button {
  background-color: #fff !important;
  color: #dc3545 !important;
  border: 1px solid #dc3545 !important;
  font-size: 14px !important;
  font-weight: 500 !important;
  border-radius: 4px !important;
  padding: 8px 16px !important;
  height: auto !important;
}

// SECONDARY BUTTON (Grey background)
.button.secondary-button {
  background-color: #f8f9fa !important;
  color: #212529 !important;
  border: 1px solid #dee2e6 !important;
  font-size: 14px !important;
  font-weight: 500 !important;
  border-radius: 4px !important;
  padding: 8px 16px !important;
  height: auto !important;
}

// PRIMARY STRONG BUTTON (White text on red background)
.button.primary-button-strong {
  background-color: #dc3545 !important;
  color: #fff !important;
  border: 1px solid #dc3545 !important;
  font-size: 14px !important;
  font-weight: 500 !important;
  border-radius: 4px !important;
  padding: 8px 16px !important;
  height: auto !important;
}
```

### Usage Examples

#### When user says "Make it a primary button":
- Use `class="primary-button"` 
- Results in red text and red border on white background
- Examples: Download App button, OK button in modals, connection buttons

#### When user says "Make it a secondary button":
- Use `class="secondary-button"`
- Results in grey background with dark text
- Examples: FAQ button, disconnect buttons, selected sort buttons

#### When user says "Make it a primary button strong":
- Use `class="primary-button-strong"`
- Results in white text on red background
- Examples: Sign-up button, high-emphasis CTAs

### Migration Notes

- Replace `type="is-danger"` with `class="primary-button"`
- Replace `type="is-light"` with `class="secondary-button"` for secondary actions
- Replace `type="is-black"` with `class="primary-button"` for main actions
- **REMOVED:** `danger-button` class (consolidated into `primary-button`)
- **ELIMINATED:** "Basic button" concept (use `secondary-button` instead)

### Important Notes

1. Always remove the old `type` attribute when adding the new class
2. The global styles are imported in `/src/assets/scss/theme.scss`
3. All buttons maintain consistent sizing, padding, and hover states
4. The system ensures visual consistency across the entire application
5. We now have only 3 button types (no more danger or basic buttons)

### Hover States

All button classes include hover effects:
- `primary-button`: Slightly lighter background on hover
- `secondary-button`: Slightly darker grey background on hover  
- `primary-button-strong`: Darker red background (#c82333) on hover

### Button Hierarchy

1. **Primary Button Strong** - Highest emphasis (red background, white text)
2. **Primary Button** - High emphasis (white background, red text)
3. **Secondary Button** - Medium emphasis (grey background, dark text)

This system ensures consistent, professional-looking buttons throughout the TrainerDay application with clear visual hierarchy.