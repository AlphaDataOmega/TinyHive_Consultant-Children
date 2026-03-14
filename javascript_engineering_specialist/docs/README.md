# JavaScript Engineering Specialist Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/javascript_best_practices_sop.md`

## Code Style

### Naming Conventions
| Type | Style | Example |
|------|-------|---------|
| Variables | camelCase | `userName` |
| Constants | UPPER_SNAKE | `MAX_COUNT` |
| Functions | camelCase | `getUserData` |
| Classes | PascalCase | `UserService` |

### Variable Declaration
| Keyword | Use Case |
|---------|----------|
| `const` | Default choice |
| `let` | Reassignment needed |
| `var` | Avoid |

## ES6+ Features

### Arrow Functions
```javascript
// Short syntax
const add = (a, b) => a + b;

// With body
const process = (data) => {
  const result = transform(data);
  return result;
};
```

### Destructuring
```javascript
// Object
const { name, age } = user;

// Array
const [first, ...rest] = items;

// Default values
const { id = 0 } = config;
```

## Async Programming

### Async/Await
```javascript
async function fetchData() {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return data;
  } catch (error) {
    handleError(error);
  }
}
```

### Parallel Execution
```javascript
const [users, posts] = await Promise.all([
  fetchUsers(),
  fetchPosts()
]);
```

## Error Handling

| Pattern | Use Case |
|---------|----------|
| try/catch | Sync and async |
| .catch() | Promise chains |
| Error boundary | React/component |
| Global handler | Uncaught errors |

## DOM Best Practices

| Do | Don't |
|----|-------|
| `querySelector` | `getElementById` |
| Event delegation | Many listeners |
| Batch updates | Multiple reflows |
| `textContent` | `innerHTML` (unsafe) |

## Event Handling

### Delegation
```javascript
container.addEventListener('click', (e) => {
  if (e.target.matches('.item')) {
    handleItemClick(e.target);
  }
});
```

### Throttle/Debounce
| Pattern | Use Case |
|---------|----------|
| Throttle | Scroll, resize |
| Debounce | Search input |

## Security

| Threat | Prevention |
|--------|------------|
| XSS | Sanitize input, `textContent` |
| CSRF | Tokens, SameSite cookies |
| Injection | Parameterized queries |

## Performance

| Technique | Benefit |
|-----------|---------|
| Lazy loading | Faster initial load |
| Memoization | Cache results |
| Web Workers | Off-thread work |
| Virtual scroll | Large lists |

## Related Consultants
- `javascript_specialist` - JS fundamentals
- `css_architecture_specialist` - Styling
- `web_accessibility_specialist` - A11y
