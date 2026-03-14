# Technical Interview Coach Reference

## Primary SOP
`/home/ubuntu/TinyHive-sops/development/technical_interview_sop.md`

## Core Interview Topics

### Scope & Closures
```javascript
// Closure example
function outer() {
  let count = 0;
  return function inner() {
    return ++count;
  };
}
const counter = outer();
counter(); // 1
counter(); // 2
```

### Hoisting Rules
| Declaration | Hoisted | Initialized |
|-------------|---------|-------------|
| var | Yes | undefined |
| let | Yes | TDZ |
| const | Yes | TDZ |
| function | Yes | Yes |
| function expr | Variable rules apply |

### Event Methods
| Method | Effect |
|--------|--------|
| preventDefault() | Stops default action |
| stopPropagation() | Stops bubbling/capturing |
| stopImmediatePropagation() | Stops other handlers too |

### Promise Polyfills to Know
- `Promise.all()` - All resolve or first reject
- `Promise.any()` - First resolve wins
- `Promise.allSettled()` - Wait for all, get all results
- `Promise.race()` - First to settle wins

### Common Questions
1. What is a closure?
2. Explain `this` binding
3. var vs let vs const
4. Event bubbling vs capturing
5. What is the event loop?
6. Explain prototypes
7. What are HOFs?
8. Implement debounce/throttle

### Interview Tips
1. **Think aloud** - Explain your reasoning
2. **Clarify** - Ask questions before coding
3. **Start simple** - Brute force first, optimize later
4. **Test** - Walk through examples
5. **Edge cases** - Consider boundaries

## Related Consultants
- `javascript_specialist` - Deep JS knowledge
- `career_development_advisor` - Career guidance
