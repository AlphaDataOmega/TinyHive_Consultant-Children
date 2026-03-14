# HTML/CSS Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/html_css_reference_sop.md`

## Core Knowledge Domains

### Semantic HTML Elements
| Element | Purpose |
|---------|---------|
| `<header>` | Introductory content |
| `<nav>` | Navigation links |
| `<main>` | Primary page content |
| `<article>` | Self-contained content |
| `<section>` | Thematic grouping |
| `<aside>` | Tangentially related |
| `<footer>` | Footer information |

### Flexbox Quick Reference
```css
.container {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

.item {
  flex: 1 1 auto; /* grow shrink basis */
}
```

### CSS Grid Quick Reference
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 20px;
}

.item {
  grid-column: span 2;
}
```

### Responsive Breakpoints
| Name | Width | Target |
|------|-------|--------|
| sm | 576px | Mobile landscape |
| md | 768px | Tablet |
| lg | 1024px | Desktop |
| xl | 1280px | Large desktop |

### CSS Custom Properties
```css
:root {
  --color-primary: #2563eb;
  --spacing-md: 1rem;
  --border-radius: 0.5rem;
}

.button {
  background: var(--color-primary);
  padding: var(--spacing-md);
  border-radius: var(--border-radius);
}
```

## Related Consultants
- `javascript_specialist` - Frontend logic
- `web_accessibility_specialist` - A11y considerations
