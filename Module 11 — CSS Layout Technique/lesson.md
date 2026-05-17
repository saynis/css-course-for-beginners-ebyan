# Module 13 — CSS Layout Techniques

> **Section:** Advanced
> **Est. Time:** 6 hours
> **Goal:** Build powerful, responsive layouts using Flexbox and CSS Grid

---

## The Big Picture

Before Flexbox and Grid, CSS layout was a hack — we used floats, tables, and inline-block tricks. Today, we have two purpose-built layout systems:

- **Flexbox** — One-dimensional layout (a row OR a column)
- **CSS Grid** — Two-dimensional layout (rows AND columns)

---

# PART 1: FLEXBOX

## Lesson 13.1 — What is Flexbox?

Flexbox makes it easy to arrange items in a row or column, align them, and distribute space. It's the go-to for component-level layout.

**How to activate it:**

```css
.container {
  display: flex;
}
/* All direct children are now "flex items" */
```

---

## Lesson 13.2 — Flex Direction

Controls the direction items are arranged.

```css
.container {
  display: flex;
  flex-direction: row;         /* Default: left → right */
  flex-direction: row-reverse; /* Right → left */
  flex-direction: column;      /* Top → bottom */
  flex-direction: column-reverse; /* Bottom → top */
}
```

---

## Lesson 13.3 — Justify Content

Controls alignment along the **main axis** (the direction items flow).

```css
.container {
  display: flex;
  justify-content: flex-start;    /* Default: items at start */
  justify-content: flex-end;      /* Items at end */
  justify-content: center;        /* Items centered */
  justify-content: space-between; /* First and last at edges, space between */
  justify-content: space-around;  /* Equal space around each item */
  justify-content: space-evenly;  /* Perfectly equal gaps everywhere */
}
```

---

## Lesson 13.4 — Align Items

Controls alignment along the **cross axis** (perpendicular to the direction items flow).

```css
.container {
  display: flex;
  align-items: stretch;     /* Default: items stretch to fill */
  align-items: flex-start;  /* Items align to start */
  align-items: flex-end;    /* Items align to end */
  align-items: center;      /* Items centered */
}
```

**Centering something perfectly:**

```css
.center-everything {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
}
```

---

## Lesson 13.5 — Flex Wrap

By default, flex items stay in one line. `flex-wrap` lets them wrap to the next line.

```css
.container {
  display: flex;
  flex-wrap: nowrap;   /* Default: stay on one line */
  flex-wrap: wrap;     /* Wrap to next line when needed */
}
```

---

## Lesson 13.6 — Gap

Space between flex items.

```css
.container {
  display: flex;
  gap: 16px;           /* Equal gap between all items */
  gap: 16px 24px;      /* Row gap | Column gap */
  row-gap: 16px;
  column-gap: 24px;
}
```


### Individual Alignment with `align-self`

Override `align-items` for one specific item:

```css
.container {
  display: flex;
  align-items: center; /* All items centered */
}

.special-item {
  align-self: flex-end; /* This one aligns to the bottom */
}
```

---

## Flexbox Navigation Example

```html
<nav class="navbar">
  <div class="nav-logo">Brand</div>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Work</a></li>
  </ul>
  <div class="nav-cta">
    <a href="#" class="btn">Contact</a>
  </div>
</nav>
```

```css
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 32px;
  background: #1a202c;
}

.nav-logo {
  color: white;
  font-size: 1.5rem;
  font-weight: 700;
}

.nav-links {
  display: flex;
  list-style: none;
  gap: 32px;
}

.nav-links a {
  color: rgba(255,255,255,0.8);
  text-decoration: none;
}

.btn {
  background: #667eea;
  color: white;
  padding: 8px 20px;
  border-radius: 6px;
  text-decoration: none;
}
```

---

## Card Grid with Flexbox

```css
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 24px;
}

```

---

# PART 2: CSS GRID

## Lesson 13.8 — What is CSS Grid?

Grid is for **two-dimensional** layout — rows and columns at the same time. Use it for page-level layouts.

```css
.container {
  display: grid;
}
```

---

## Lesson 13.9 — Defining Rows and Columns

```css
.grid {
  display: grid;

  /* 3 equal columns */
  grid-template-columns: 1fr 1fr 1fr;

  /* Shorthand */
  grid-template-columns: repeat(3, 1fr);

  /* Mixed sizes */
  grid-template-columns: 250px 1fr 1fr;  /* Sidebar + 2 columns */
  grid-template-columns: 1fr 2fr 1fr;    /* Middle column twice as wide */

  /* Define rows */
  grid-template-rows: 80px 1fr 60px; /* Header, content, footer */

  /* Gaps */
  gap: 24px;
  column-gap: 32px;
  row-gap: 16px;
}
```

**What is `fr`?** Fractional unit — represents a fraction of the available space.

```css
grid-template-columns: 1fr 2fr 1fr;
/* Column 2 gets twice as much space as columns 1 and 3 */
```

---

## Lesson 13.10 — `repeat()` and `minmax()`

```css
/* repeat(count, size) */
grid-template-columns: repeat(4, 1fr);   /* 4 equal columns */
grid-template-columns: repeat(3, 200px); /* 3 fixed-width columns */

/* minmax(min, max) — column is at least 250px, at most 1fr */
grid-template-columns: repeat(3, minmax(250px, 1fr));

/* Auto-fill: fit as many columns as possible */
grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));

/* Auto-fit: similar but collapses empty columns */
grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
```

`auto-fill` and `auto-fit` with `minmax` create **responsive grids without media queries**!



## Lesson 13.13 — Alignment in Grid

```css
.grid {
  /* Align all items */
  justify-items: center;  /* Horizontal alignment */
  align-items: center;    /* Vertical alignment */

  /* Center the entire grid */
  justify-content: center;
  align-content: center;
}

.item {
  /* Align individual item */
  justify-self: center;
  align-self: end;
}
```

---

## Real-World Grid Layouts

### Responsive Photo Gallery

```css
.gallery {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
  gap: 16px;
}

.gallery-item img {
  width: 100%;
  height: 240px;
  object-fit: cover;
  border-radius: 8px;
}
```
---

# PART 3: WHEN TO USE WHAT

| Situation | Use |
|-----------|-----|
| Navbar (horizontal items) | Flexbox |
| Cards in a row | Flexbox |
| Center content | Flexbox |
| Page structure (header, sidebar, content, footer) | Grid |
| Photo gallery | Grid |
| Dashboard layout | Grid |
| Items in a single line | Flexbox |
| Items that need to align in both axes | Grid |

> **In practice:** Use them together! Grid for page layout, Flexbox for components inside grid areas.

---

## ⚠️ Important Notes

- Flexbox and Grid are not mutually exclusive — use both on the same page
- `gap` works in both Flexbox and Grid
- `auto-fit` + `minmax` is the most powerful responsive grid pattern — memorize it

## 🧪 Mini Practice Task

**Flexbox:** Build a horizontal navbar with the logo on the left, links in the center, and a button on the right.

**Grid:** Build a 3-column responsive card grid that auto-reflows on smaller screens (using `auto-fit` + `minmax`).

## 📝 Homework Assignment

Build a **Personal Portfolio Layout** with:
- A fixed navbar using Flexbox
- A hero section using Flexbox (centered content)
- A "Projects" section using CSS Grid with auto-responsive columns
- A blog preview section with a large featured post (spanning 2 columns) and smaller posts
- A footer with 4 columns using Grid, that stacks to 2 on medium screens

---

*Next up → [Module 12: Media Queries & Responsive Design](../module-12-Media Queries/lesson.md)*