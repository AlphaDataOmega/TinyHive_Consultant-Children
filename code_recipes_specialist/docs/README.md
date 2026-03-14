# Code Recipes Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/code_recipes_sop.md`

## Core Recipes

### UI Components
| Component | Key Features |
|-----------|--------------|
| Dropdown | Multi-level, keyboard nav, ARIA |
| Tooltip | Adaptive positioning, anchor API |
| Slider | Carousel, keyboard support |
| Popup | Native `<dialog>`, focus trap |
| Progress | Upload progress bar |

### Form Patterns
| Pattern | Implementation |
|---------|----------------|
| Validation | Real-time, instant feedback |
| Checkbox/Radio | 3 styling methods |
| Range Input | Dual handle support |
| Character Counter | Live count display |
| Ajax Form | Async submission |

### Layout Patterns
| Pattern | Method |
|---------|--------|
| Center Horizontal | `margin: auto` |
| Center Both | Flexbox/Grid |
| Container | `clamp()` for fluid width |
| Masonry | Flexbox approach |

### Code Example: Accessible Dropdown
```html
<nav aria-label="Main">
  <ul role="menubar">
    <li role="none">
      <a href="#" role="menuitem" aria-haspopup="true" aria-expanded="false">
        Menu
      </a>
      <ul role="menu">
        <li role="none">
          <a href="#" role="menuitem">Item</a>
        </li>
      </ul>
    </li>
  </ul>
</nav>
```

### Accessibility Checklist
- [ ] Keyboard navigation works
- [ ] Focus is visible
- [ ] ARIA attributes present
- [ ] Screen reader tested
- [ ] Color contrast passes

## Related Consultants
- `html_css_specialist` - Layout and styling
- `javascript_specialist` - JS implementation
- `web_accessibility_specialist` - A11y review
