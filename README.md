# Css theory (part 6)
## Q6: What is CSS Specificity and How Does the Cascade Work?

### Introduction

When multiple CSS rules target the same HTML element, the browser must decide which rule should be applied. CSS uses a system called **Specificity** and **Cascade** to determine which style wins.

Understanding specificity and the cascade is important because it helps developers write cleaner CSS, avoid conflicts, and control how styles are applied to web pages.

---

## What is CSS Specificity?

**Specificity** is a scoring system used by browsers to determine which CSS rule has higher priority when multiple rules target the same element.

The rule with the **highest specificity value** will be applied.

### Specificity Hierarchy

The priority order from highest to lowest is:

| Selector Type | Specificity Value |
|--------------|------------------|
| Inline Style | 1000 |
| ID Selector | 100 |
| Class Selector | 10 |
| Element Selector | 1 |
| Universal Selector (*) | 0 |

### Example

```html
<p id="intro" class="text">Hello World</p>
```

```css
p {
    color: blue;
}

.text {
    color: green;
}

#intro {
    color: red;
}
```

### Result

The text will be **red** because the ID selector (`#intro`) has a higher specificity score than the class selector (`.text`) and the element selector (`p`).

---

## Which Has Higher Specificity: Class or Element Selector?

A **Class Selector** has higher specificity than an **Element Selector**.

### Example

```html
<p class="text">Hello</p>
```

```css
p {
    color: blue;
}

.text {
    color: green;
}
```

### Result

The text becomes **green** because:

- Element Selector = 1
- Class Selector = 10

Since 10 is greater than 1, the class selector wins.

---

## What Specificity Score Does an Inline Style Have?

Inline styles have the highest normal specificity.

### Example

```html
<p style="color:red;" class="text">
    Hello World
</p>
```

```css
.text {
    color: green;
}
```

### Result

The text will be **red** because inline styles have a specificity score of **1000**, which is higher than class selectors.

---

## What is the CSS Cascade?

The **Cascade** is the process browsers use to determine which CSS rule should be applied when multiple rules affect the same element.

The cascade considers:

1. Importance (`!important`)
2. Specificity
3. Source Order
4. Inheritance

---

## 1. Importance

Rules marked with `!important` have higher priority than normal CSS rules.

### Example

```css
p {
    color: blue !important;
}

#intro {
    color: red;
}
```

### Result

The text becomes **blue** because the `!important` rule overrides the ID selector.

---

## 2. Specificity

If no `!important` rule exists, the browser compares specificity scores.

### Example

```css
p {
    color: blue;
}

.text {
    color: green;
}

#intro {
    color: red;
}
```

### Result

The ID selector wins because it has the highest specificity.

---

## 3. Source Order

If two selectors have the same specificity, the rule written later in the CSS file wins.

### Example

```css
.text {
    color: blue;
}

.text {
    color: green;
}
```

### Result

The text becomes **green** because the second rule appears later in the stylesheet.

---

## 4. Inheritance

Some CSS properties automatically pass from parent elements to their children.

### Example

```html
<div>
    <p>Hello World</p>
</div>
```

```css
div {
    color: blue;
}
```

### Result

The paragraph inherits the blue color from the parent `<div>`.

---

## What Does !important Do?

The `!important` keyword forces a CSS rule to have the highest priority among normal styles.

### Example

```css
#intro {
    color: red;
}

.text {
    color: green !important;
}
```

### Result

The text becomes **green** because the `!important` rule overrides the ID selector.

---

## Why Should !important Be Avoided?

Although `!important` can solve styling conflicts, excessive use creates maintenance problems.

### Disadvantages

- Makes debugging difficult
- Breaks normal specificity rules
- Creates CSS conflicts
- Reduces code readability
- Makes projects harder to maintain

### Best Practice

Use proper selectors and specificity instead of relying on `!important` whenever possible.

---

## Code Task

### HTML

```html
<p id="intro" class="text">Hello</p>
```

### CSS

```css
p {
    color: blue;
}

.text {
    color: green;
}

#intro {
    color: red;
}
```

### Specificity Calculation

| Selector | Specificity |
|----------|------------|
| p | 1 |
| .text | 10 |
| #intro | 100 |

### Which Color Wins?

The final color will be **red** because:

- `p` selector = 1
- `.text` selector = 10
- `#intro` selector = 100

Since the ID selector has the highest specificity score, its style is applied.

---

## Key Takeaways

- CSS Specificity determines which rule has higher priority.
- Inline styles have the highest normal specificity (1000).
- ID selectors are stronger than class selectors.
- Class selectors are stronger than element selectors.
- If specificity is equal, the rule written later wins.
- The Cascade combines importance, specificity, source order, and inheritance.
- `!important` overrides normal specificity rules.
- Avoid excessive use of `!important` to keep CSS maintainable.

---

## Conclusion

CSS Specificity and the Cascade work together to decide which styles are applied to an element. Specificity assigns a priority score to selectors, while the Cascade considers importance, specificity, source order, and inheritance. Understanding these concepts helps developers write cleaner, more predictable, and maintainable CSS code.