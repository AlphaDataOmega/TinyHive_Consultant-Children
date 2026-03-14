# Web Accessibility Specialist Reference

## Primary SOP
Based on Doka Guide Accessibility Documentation (436 files)

## Core Knowledge Domains

### ARIA Roles
| Category | Examples |
|----------|----------|
| Landmark | banner, main, navigation, contentinfo |
| Widget | button, checkbox, slider, tab |
| Structure | list, listitem, table, row |
| Live Region | alert, status, log, timer |

### ARIA States & Properties
```html
<!-- States (change during interaction) -->
aria-expanded="true|false"
aria-selected="true|false"
aria-checked="true|false|mixed"
aria-disabled="true|false"
aria-hidden="true|false"

<!-- Properties (generally static) -->
aria-label="Accessible name"
aria-labelledby="element-id"
aria-describedby="description-id"
aria-required="true"
aria-invalid="true|false"
```

### WCAG Success Criteria (Level AA)
| Principle | Key Requirements |
|-----------|-----------------|
| Perceivable | Alt text, captions, contrast 4.5:1 |
| Operable | Keyboard access, focus visible, no seizures |
| Understandable | Readable, predictable, input assistance |
| Robust | Compatible with assistive tech |

### Screen Reader Shortcuts
- **Headings**: H (next), Shift+H (previous)
- **Landmarks**: D (next region)
- **Links**: K (next link)
- **Forms**: F (next form control)
- **Tables**: T (next table)

### Focus Management
```javascript
// Set focus programmatically
element.focus();

// Trap focus in modal
const focusableElements = modal.querySelectorAll(
  'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
);
```

## Related Consultants
- `html_css_specialist` - Semantic HTML
- `javascript_specialist` - Dynamic accessibility
