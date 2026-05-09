---
layout: minimal
title: JavaScript Code Quality
nav_enabled: true
parent: Open Source Projects
nav_order: 6
---
## JavaScript

### Core Principles

- **Vanilla first.** Use the DOM API, Fetch API, and Web APIs before adding libraries.
- **Progressive enhancement.** The page works without JS. JS adds behaviour.
- **Modules everywhere.** Use ES modules (`type="module"`) for all non-trivial scripts.
- **No global scope pollution.** Nothing should live on `window` intentionally.

### File Structure

```
js/
├── main.js           # Entry point — imports and init only
├── modules/
│   ├── dom.js        # DOM helpers
│   ├── api.js        # Fetch wrappers
│   └── utils.js      # Pure utility functions
└── components/
    ├── modal.js
    └── form-validation.js
```

### Naming Conventions

| Type | Convention | Example |
|------|------------|---------|
| Variables | `camelCase` | `userCount`, `fetchedData` |
| Constants | `UPPER_SNAKE_CASE` | `MAX_RETRIES`, `API_BASE_URL` |
| Functions | `camelCase`, verb-first | `fetchUser()`, `handleSubmit()` |
| Classes | `PascalCase` | `ModalDialog`, `FormValidator` |
| Private fields | `#` prefix (native) | `#cache`, `#isOpen` |
| Files | `kebab-case` | `form-validation.js`, `modal.js` |

### Variables & Scoping

```javascript
// Bad — var is function-scoped and hoisted
var count = 0;

// Good — const by default
const MAX_RETRIES = 3;
const user = { name: 'alice' };  // const for object references too

// let only when reassignment is genuinely needed
let attempt = 0;
while (attempt < MAX_RETRIES) {
    attempt++;
}
```

### Functions

Prefer named function declarations for top-level functions (hoisting aids readability). Arrow functions for callbacks and inline expressions.

```javascript
// Top-level: named declaration
function fetchUser(id) {
    // ...
}

// Callback: arrow function
const activeUsers = users.filter(user => user.active);

// Event handler: named for debugging (shows up in stack traces)
button.addEventListener('click', handleButtonClick);

function handleButtonClick(event) {
    event.preventDefault();
    // ...
}
```

### Error Handling

```javascript
// Always handle promise rejections
async function loadUserData(id) {
    try {
        const response = await fetch(`/api/users/${id}`);

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        return await response.json();
    } catch (error) {
        console.error(`loadUserData failed for id=${id}:`, error);
        throw error; // re-throw unless you're handling it here
    }
}

// Catch at the call site when you can do something about it
async function renderUserProfile(id) {
    try {
        const user = await loadUserData(id);
        renderProfile(user);
    } catch (error) {
        showErrorMessage('Could not load profile. Please try again.');
    }
}
```

### DOM Interaction

```javascript
// Query once, reuse reference
const form = document.querySelector('#signup-form');
const submitButton = form.querySelector('[type="submit"]');

// Bad — requerying on each call
function handleInput() {
    document.querySelector('#signup-form').classList.add('dirty');
}

// Good — closed over reference
function handleInput() {
    form.classList.add('dirty');
}

// Event delegation for dynamic content
document.querySelector('.card-list').addEventListener('click', (event) => {
    const card = event.target.closest('.card');
    if (!card) return;
    handleCardClick(card);
});

// Prefer dataset over custom attributes for JS hooks
// HTML: <button data-action="delete" data-id="42">
const action = event.target.dataset.action;
const id = event.target.dataset.id;
```

### Modules

```javascript
// utils.js — pure functions, no side effects
export function clamp(value, min, max) {
    return Math.min(Math.max(value, min), max);
}

export function debounce(fn, delayMs) {
    let timer;
    return (...args) => {
        clearTimeout(timer);
        timer = setTimeout(() => fn(...args), delayMs);
    };
}

// api.js — fetch wrappers
const API_BASE_URL = '/api/v1';

export async function get(path) {
    const response = await fetch(`${API_BASE_URL}${path}`);
    if (!response.ok) {
        throw new Error(`GET ${path} failed: ${response.status}`);
    }
    return response.json();
}

// main.js — entry point, wires everything
import { debounce } from './modules/utils.js';
import { get } from './modules/api.js';

document.addEventListener('DOMContentLoaded', init);

function init() {
    const searchInput = document.querySelector('#search');
    searchInput.addEventListener('input', debounce(handleSearch, 300));
}
```

---

## Power of 10 — JavaScript Adaptation

### 1. Simple Control Flow

No `eval()`. No `new Function()`. Avoid deeply nested callbacks — use `async/await`.

```javascript
// Bad — callback hell
fetchUser(id, (err, user) => {
    if (err) return handleError(err);
    fetchOrders(user.id, (err, orders) => {
        if (err) return handleError(err);
        renderPage(user, orders);
    });
});

// Good — async/await, linear flow
async function loadPage(id) {
    const user = await fetchUser(id);
    const orders = await fetchOrders(user.id);
    renderPage(user, orders);
}
```

### 2. Fixed Loop Bounds

```javascript
const MAX_RETRIES = 5;

for (let attempt = 0; attempt < MAX_RETRIES; attempt++) {
    const result = await tryOperation();
    if (result.success) break;
    if (attempt === MAX_RETRIES - 1) {
        throw new Error(`Operation failed after ${MAX_RETRIES} attempts`);
    }
}
```

### 3. Bounded Data Structures

```javascript
const MAX_CACHE_SIZE = 200;

class BoundedCache {
    #store = new Map();
    #maxSize;

    constructor(maxSize = MAX_CACHE_SIZE) {
        this.#maxSize = maxSize;
    }

    set(key, value) {
        if (this.#store.size >= this.#maxSize) {
            // Evict oldest entry (Maps maintain insertion order)
            const firstKey = this.#store.keys().next().value;
            this.#store.delete(firstKey);
        }
        this.#store.set(key, value);
    }

    get(key) {
        return this.#store.get(key);
    }
}
```

### 4. Short Functions

Max ~30 lines for JavaScript functions. Separate DOM manipulation from data logic. A function that fetches, transforms, and renders is three functions.

### 5. High Assertion via Guard Clauses

```javascript
function renderUserCard(user) {
    if (!user) throw new TypeError('renderUserCard: user is required');
    if (typeof user.name !== 'string') throw new TypeError('renderUserCard: user.name must be a string');
    if (!user.id) throw new TypeError('renderUserCard: user.id is required');

    // logic here
}
```

### 6. Minimal Variable Scope

Declare variables in the narrowest block that needs them. Avoid module-level mutable state.

```javascript
// Bad — outer scope mutation
let result;
if (condition) {
    result = computeA();
} else {
    result = computeB();
}

// Good — block scoped
const result = condition ? computeA() : computeB();
```

### 7. Check All Return Values

```javascript
// Bad — assuming success
const data = JSON.parse(rawInput);

// Good — guarded
let data;
try {
    data = JSON.parse(rawInput);
} catch (error) {
    console.error('Failed to parse input:', error);
    return null;
}

// Bad — unchecked querySelector
document.querySelector('.submit-btn').addEventListener('click', handler);

// Good — guard against missing element
const submitBtn = document.querySelector('.submit-btn');
if (!submitBtn) {
    console.warn('submit button not found — skipping handler');
    return;
}
submitBtn.addEventListener('click', handler);
```

### 8. Limit Metaprogramming

No `eval()`, `new Function()`, or `with` statements. Avoid `Proxy` and `Reflect` outside library code. Use `Object.freeze()` for truly immutable constants.

```javascript
// Bad
eval(userProvidedCode);

// Bad — dynamic property access as a dispatch table
function dispatch(action) {
    this[action](); // eval-adjacent, unanalyzable
}

// Good — explicit dispatch
const handlers = {
    submit: handleSubmit,
    reset: handleReset,
    cancel: handleCancel,
};

function dispatch(action) {
    const handler = handlers[action];
    if (!handler) throw new Error(`Unknown action: ${action}`);
    handler();
}
```

### 9. Limit Data Structure Nesting

Flatten deeply nested objects. If you're accessing `data.response.user.profile.settings.theme`, introduce an intermediate variable or refactor the data shape.

```javascript
// Bad
const theme = config.ui.preferences.display.colors.theme;

// Good — destructure at point of use
const { theme } = config.ui.preferences.display.colors;

// Better — flatten the data structure at the source
const displaySettings = {
    theme: 'dark',
    fontSize: 14,
    contrast: 'high',
};
```

### 10. Enable All Static Analysis

```json
// .eslintrc.json
{
    "env": { "browser": true, "es2022": true },
    "parserOptions": { "ecmaVersion": "latest", "sourceType": "module" },
    "rules": {
        "no-eval": "error",
        "no-implied-eval": "error",
        "no-new-func": "error",
        "no-var": "error",
        "prefer-const": "error",
        "eqeqeq": ["error", "always"],
        "no-unused-vars": ["error", { "argsIgnorePattern": "^_" }],
        "no-undef": "error",
        "curly": "error",
        "no-console": "warn"
    }
}
```

---

## Quick Reference Tables

### Go

| Rule | Guidance |
|------|----------|
| Simple control flow | No `goto`; iterate, don't recurse; depth-guard if needed |
| Fixed loop bounds | `for i := range MAX` or explicit bound with error at limit |
| Bounded data | Buffered channels with capacity; `lru.New[K,V](maxSize)` |
| Short functions | ≤50 lines; single responsibility |
| Assertion density | Validate inputs; check postconditions; use `errors.Is/As` |
| Minimal scope | `:=` in narrowest block; no package-level mutable state |
| Check returns | Never `_` an error without a comment; always check `ok` |
| Limit metaprogramming | Avoid `reflect`/`unsafe`; minimal `any` usage |
| Limit nesting | ≤3 levels; structs over nested maps |
| Static analysis | `golangci-lint run`; `go test -race ./...` in CI |

### JavaScript / HTML / CSS

| Rule | Guidance |
|------|----------|
| Simple control flow | `async/await` over callbacks; no `eval`/`new Function` |
| Fixed loop bounds | `for` with explicit count; `MAX_RETRIES` constant |
| Bounded data | `BoundedCache` pattern; `maxSize` on all collections |
| Short functions | ≤30 lines; separate fetch / transform / render |
| Assertion density | Guard clauses at function entry; check `querySelector` results |
| Minimal scope | `const` default; `let` only for reassignment; no `var` |
| Check returns | Guard every `querySelector`; wrap `JSON.parse` in try/catch |
| Limit metaprogramming | No `eval`; explicit dispatch tables over dynamic dispatch |
| Limit nesting | ≤3 levels; destructure at use site |
| Static analysis | ESLint strict config; lint as CI gate |

# API Standards

- APIs must be versioned
- Use consistent error response structures
- Prefer idempotent operations where possible
- Return structured errors with machine-readable codes
- Validate request schemas strictly

```json
{
  "error": {
    "code": "USER_NOT_FOUND",
    "message": "User does not exist"
  }
}
```