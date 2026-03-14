# CSS Architecture Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/css_reference_guide_sop.md`

## CSS Architecture

### BEM Naming
| Element | Pattern | Example |
|---------|---------|---------|
| Block | `.block` | `.card` |
| Element | `.block__element` | `.card__title` |
| Modifier | `.block--modifier` | `.card--featured` |

### OOCSS Principles
| Principle | Description |
|-----------|-------------|
| Separate structure | Layout vs skin |
| Separate container | Content independent |

## Layout Systems

### Flexbox
| Property | Values |
|----------|--------|
| `display` | `flex` |
| `flex-direction` | `row`, `column` |
| `justify-content` | `start`, `center`, `space-between` |
| `align-items` | `start`, `center`, `stretch` |
| `gap` | spacing value |

### Grid
| Property | Values |
|----------|--------|
| `display` | `grid` |
| `grid-template-columns` | `repeat(3, 1fr)` |
| `grid-gap` | spacing value |
| `grid-area` | named areas |

## Responsive Design

### Breakpoints
| Name | Width | Target |
|------|-------|--------|
| sm | 640px | Mobile |
| md | 768px | Tablet |
| lg | 1024px | Desktop |
| xl | 1280px | Large |

### Mobile-First
```css
/* Base: mobile */
.element { width: 100%; }

/* Tablet and up */
@media (min-width: 768px) {
  .element { width: 50%; }
}
```

## CSS Custom Properties

```css
:root {
  --color-primary: #3b82f6;
  --spacing-md: 1rem;
  --font-size-base: 16px;
}

.element {
  color: var(--color-primary);
  padding: var(--spacing-md);
}
```

## Dark Mode

```css
:root {
  --bg: white;
  --text: black;
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg: #1a1a1a;
    --text: white;
  }
}
```

## Accessibility

| Requirement | Implementation |
|-------------|---------------|
| Focus visible | `outline` on `:focus-visible` |
| Reduced motion | `@media (prefers-reduced-motion)` |
| Contrast | 4.5:1 minimum |
| Touch targets | 44px minimum |

## Performance

| Technique | Benefit |
|-----------|---------|
| Critical CSS | Faster FCP |
| `contain` | Isolation |
| `will-change` | GPU acceleration |
| Font display | Text visibility |

## Related Consultants
- `html_css_specialist` - HTML/CSS fundamentals
- `web_accessibility_specialist` - Accessibility
- `javascript_engineering_specialist` - Frontend JS
