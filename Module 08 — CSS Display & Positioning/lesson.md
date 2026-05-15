# Module 08 — CSS Display & Positioning

> **Section:** Beginner
> **Est. Time:** 4 hours
> **Goal:** Control how elements flow on the page and where they sit

---

## Lesson 8.1 — Block vs. Inline Elements

HTML elements have a default `display` value. The two most common are **block** and **inline**.

### Block Elements

- Take up the **full width** of their parent
- Start on a **new line**
- Respect `width`, `height`, `margin`, `padding`
- Examples: `<div>`, `<p>`, `<h1>–<h6>`, `<section>`, `<article>`, `<ul>`, `<li>`

```html
<p>First paragraph — takes full width, starts on new line.</p>
<p>Second paragraph — automatically drops to next line.</p>
```

### Inline Elements

- Only take up **as much width as their content**
- Stay **on the same line** as adjacent elements
- `width` and `height` have no effect
- Vertical `margin` and `padding` behave unexpectedly
- Examples: `<span>`, `<a>`, `<strong>`, `<em>`, `<img>`

```html
<p>This is <strong>bold</strong> and <em>italic</em> — all on the same line.</p>
```

---

## Lesson 8.2 — The `display` Property

You can change any element's default display behavior.

```css
/* Common values */
display: block;         /* Full-width, new line */
display: inline;        /* In-line, no width/height */
display: inline-block;  /* In-line but respects width/height */
display: none;          /* Hides the element completely */
display: flex;          /* Flexbox container (Module 13) */
display: grid;          /* Grid container (Module 13) */
```

### `inline-block` — The Best of Both Worlds

Makes an element flow inline but lets you set `width`, `height`, and vertical margins.

```css
/* Navigation links side by side */
.nav-link {
  display: inline-block;
  padding: 8px 16px;
  background: #333;
  color: white;
  text-decoration: none;
}
```

### `display: none`

Completely removes the element from the page (it takes up no space).

```css
.hidden { display: none; }

/* Show/hide on mobile — we'll use this with media queries */
.mobile-menu { display: none; }
```

> **Difference from `visibility: hidden`:** `display: none` removes the element from flow. `visibility: hidden` hides it but the space remains.

---

## Lesson 8.3 — The `position` Property

The `position` property controls how an element is placed within the page flow.

---

### `position: static` (Default)

Elements flow normally. `top`, `left`, `right`, `bottom` have no effect.

```css
div { position: static; } /* This is the default */
```

---

### `position: relative`

The element stays in normal flow, but you can **nudge it** using `top`, `left`, `right`, `bottom`. The space it occupied remains.

```css
.nudged {
  position: relative;
  top: 10px;    /* Move 10px down from normal position */
  left: 20px;   /* Move 20px right from normal position */
}
```

**Most common use:** As a **positioning context** for absolutely positioned children.

---

### `position: absolute`

The element is **removed from normal flow** — other elements ignore it. It positions itself relative to the nearest **positioned ancestor** (an ancestor with `position` anything other than `static`).

```css
.parent {
  position: relative; /* Makes this the positioning context */
  width: 300px;
  height: 200px;
}

.badge {
  position: absolute;
  top: 10px;
  right: 10px;
  /* Now positioned 10px from top-right of .parent */
}
```

**Common use:** Overlays, badges, tooltips, dropdowns.

```html
<div class="card">
  <img src="product.jpg" alt="">
  <span class="badge">NEW</span>
</div>
```

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 12px;
  left: 12px;
  background: red;
  color: white;
  padding: 4px 10px;
  border-radius: 20px;
  font-size: 0.75rem;
  font-weight: 700;
}
```

---

### `position: fixed`

Positioned relative to the **browser window** — doesn't scroll with the page.

```css
/* Sticky navigation bar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  background: white;
  z-index: 100;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

/* Floating "back to top" button */
.back-to-top {
  position: fixed;
  bottom: 30px;
  right: 30px;
}
```

---

### `position: sticky`

The element scrolls normally **until** it hits a defined threshold, then sticks.

```css
/* Sticky header that sticks when you scroll to it */
.section-header {
  position: sticky;
  top: 0;
  background: white;
  padding: 16px;
  z-index: 10;
}
```

---

## Lesson 8.4 — `z-index`

Controls the **stacking order** of positioned elements. Higher = on top.

```css
.modal {
  position: fixed;
  z-index: 1000;  /* On top of everything */
}

.navbar {
  position: fixed;
  z-index: 100;   /* Above content, but below modal */
}

.dropdown {
  position: absolute;
  z-index: 50;    /* Above regular content */
}
```

> **Key rule:** `z-index` only works on positioned elements (not `static`).

---

## Lesson 8.5 — Floats & Clearfix

Floats are an older layout technique. You'll mostly use Flexbox and Grid now, but floats still appear in legacy code.

```css
img {
  float: left;         /* Image floats left, text wraps around it */
  margin-right: 16px;
  margin-bottom: 8px;
}

.sidebar {
  float: right;
  width: 30%;
}

.main-content {
  float: left;
  width: 65%;
}
```


```html
<div class="clearfix">
  <div style="float: left;">Left column</div>
  <div style="float: right;">Right column</div>
</div>
<!-- The parent now wraps both floated children correctly -->
```

> **Today:** Use Flexbox or Grid instead of floats for layout. Floats are really only good for wrapping text around an image.

---

## Complete Positioning Example — Card with Badge + Sticky Nav

```html
<nav class="navbar">
  <div class="nav-logo">MyBrand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>

<div class="card">
  <img src="jacket.jpg" alt="Jacket">
  <span class="badge">SALE</span>
  <div class="card-info">
    <h3>Winter Jacket</h3>
    <p>$49.99 <s>$79.99</s></p>
  </div>
</div>
```

```css
/* Sticky navbar */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 60px;
  background: #1a202c;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 32px;
  z-index: 100;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 24px;
}

.nav-links a {
  color: white;
  text-decoration: none;
}

/* Card with badge */
.card {
  position: relative;   /* Positioning context for the badge */
  width: 280px;
  border-radius: 12px;
  overflow: hidden;
  margin-top: 80px;     /* Clear the fixed navbar */
}

.card img {
  width: 100%;
  height: 300px;
  object-fit: cover;
}

.badge {
  position: absolute;
  top: 12px;
  right: 12px;
  background: #e53e3e;
  color: white;
  padding: 4px 12px;
  border-radius: 20px;
  font-size: 0.7rem;
  font-weight: 800;
  letter-spacing: 0.05em;
}

.card-info {
  padding: 16px;
  background: white;
}
```

---

## ⚠️ Important Notes

- `z-index` requires a `position` value other than `static` to work
- `position: absolute` elements look for their nearest **positioned ancestor** — make sure to set `position: relative` on the parent
- Avoid using floats for layout — use Flexbox or Grid

## ❌ Common Beginner Mistakes

```css
/* ❌ z-index on a static element — has no effect */
.element {
  z-index: 999; /* Doesn't work! */
}

/* ✅ Must have a position value */
.element {
  position: relative;
  z-index: 999; /* Works now */
}
```

```css
/* ❌ Forgetting position: relative on parent for absolute child */
.card {
  /* No position set */
}

.badge {
  position: absolute;
  top: 0; right: 0;
  /* Now it's relative to the page, not the card! */
}

/* ✅ Fix */
.card { position: relative; }
.badge { position: absolute; top: 0; right: 0; }
```



## 📝 Homework Assignment

Build a **Product Showcase** page:
- Fixed navbar with logo and 3 links
- A hero section (full height) with centered content
- A products grid with 4 cards
  - Each card: image, product name, price, "Add to Cart" button
  - Each card has a "SALE" or "NEW" badge positioned absolutely in the corner
- A floating customer service button fixed at the bottom-right

---

*Next up → [Module 09: CSS Overflow](../module-09-overflow/lesson.md)*