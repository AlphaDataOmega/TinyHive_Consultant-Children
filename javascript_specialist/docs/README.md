# JavaScript Specialist Reference

## Primary SOP
Based on Doka Guide JavaScript Documentation (901 files)

## Core Knowledge Domains

### Data Types
| Type | Description |
|------|-------------|
| String | Text data |
| Number | Numeric values |
| Boolean | true/false |
| null | Intentional absence |
| undefined | Uninitialized |
| Symbol | Unique identifiers |
| BigInt | Large integers |
| Object | Key-value collections |

### Array Methods Quick Reference
```javascript
// Transformation
array.map(fn)      // Transform each element
array.filter(fn)   // Filter elements
array.reduce(fn)   // Reduce to single value

// Searching
array.find(fn)     // First matching element
array.findIndex(fn)// Index of first match
array.includes(x)  // Contains check

// Iteration
array.forEach(fn)  // Execute for each
array.every(fn)    // All match?
array.some(fn)     // Any match?
```

### Async Patterns
```javascript
// Promises
fetch(url)
  .then(res => res.json())
  .then(data => console.log(data))
  .catch(err => console.error(err));

// Async/Await
async function getData() {
  try {
    const res = await fetch(url);
    const data = await res.json();
    return data;
  } catch (err) {
    console.error(err);
  }
}
```

### ES6+ Features
- Arrow functions
- Template literals
- Destructuring
- Spread/rest operators
- Classes
- Modules (import/export)
- let/const
- Optional chaining (?.)
- Nullish coalescing (??)

## Related Consultants
- `html_css_specialist` - Frontend styling
- `web_accessibility_specialist` - A11y considerations
