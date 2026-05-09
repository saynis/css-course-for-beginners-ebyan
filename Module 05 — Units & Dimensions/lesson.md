# Module 05 — Units & Dimensions

> **Section:** Beginner
> **Est. Time:** 2 hours
> **Goal:** Understand how CSS measures size and when to use each unit

---

## Lesson 5.1 — Absolute Units

Absolute units are **fixed** — they don't change based on anything else.

| Unit | Full Name | Use Case |
|------|-----------|----------|
| `px` | Pixels | Most common — screen-based sizing |
| `cm`, `mm`, `in` | Physical units | Print only |

```css
/* Pixels are your main tool for fixed sizes */
.icon { width: 24px; height: 24px; }
.container { max-width: 1200px; }
.border { border: 2px solid #ddd; }
```

**When to use `px`:** Borders, fixed-width containers, icon sizes, spacing in components.

---

## Lesson 5.2 — Relative Units

Relative units **change based on something** (the parent, the root, the viewport).

---

### `em`

Relative to the **parent element's** font-size.

```css
body { font-size: 16px; }

.parent {
  font-size: 20px;
}

.child {
  font-size: 1.5em; /* 1.5 × 20px = 30px */
  padding: 1em;     /* 1 × 20px = 20px */
}
```

**Problem with `em`:** They compound (stack). If a parent is `2em` and a child is `2em`, the child is `4×` the base — often unintended.

---

### `rem` ✅ (Recommended for most sizing)

Relative to the **root element (`<html>`)** font-size — never stacks.

```css
html { font-size: 16px; } /* Base — 1rem = 16px */

h1 { font-size: 3rem; }   /* 48px */
h2 { font-size: 2rem; }   /* 32px */
p  { font-size: 1rem; }   /* 16px */

.small { font-size: 0.875rem; } /* 14px */
```

> **Best practice:** Use `rem` for font sizes and most spacing. It stays consistent regardless of nesting.

---

### Percentages

Relative to the **parent element's** corresponding property.

```css
.parent {
  width: 800px;
}

.child {
  width: 50%;    /* 50% of 800px = 400px */
  padding: 5%;   /* 5% of 800px = 40px */
}
```

**Common uses:**
```css
.container { max-width: 90%; }   /* Never wider than 90% of the viewport */
img { width: 100%; }              /* Image fills its container */
.sidebar { width: 30%; }
.main-content { width: 70%; }
```

---

### `vh` and `vw` — Viewport Units

- `vh` = 1% of the **viewport height**
- `vw` = 1% of the **viewport width**

```css
.hero {
  height: 100vh; /* Full screen height */
  width: 100vw;  /* Full screen width */
}

.half-screen {
  height: 50vh;
}
```

**Common uses:**
```css
/* Full-screen hero section */
.hero { min-height: 100vh; }

/* Sidebar that fills the screen */
.sidebar { height: 100vh; }

/* Text that scales with the screen */
h1 { font-size: 5vw; }
```

---

## Lesson 5.3 — Width & Height Best Practices

```css
/* ✅ Use max-width for containers — they flex but don't grow too wide */
.container {
  max-width: 1200px;
  width: 90%;         /* Gives padding on small screens */
  margin: 0 auto;     /* Centers the container */
}

/* ✅ Use min-height instead of height for sections */
.section {
  min-height: 400px; /* Can grow if content is taller */
}

/* ❌ Avoid fixed heights on text containers */
.card {
  height: 200px; /* Text might overflow! */
}

/* ✅ Better approach */
.card {
  min-height: 200px;
  padding: 24px; /* Space inside will push the height naturally */
}

/* ✅ Images should be responsive */
img {
  max-width: 100%;
  height: auto; /* Maintains aspect ratio */
}
```

---

## ⚠️ Important Notes

- `rem` is preferred over `em` for font sizes — no compounding confusion
- `px` is still perfectly valid for small, precise values (borders, icons, shadows)
- `vh`/`vw` are excellent for full-screen layouts
- Percentages are great for flexible, responsive widths

## ❌ Common Beginner Mistakes

```css
/* ❌ Using px for everything — not responsive */
body { font-size: 16px; }
.container { width: 1200px; } /* Will break on small screens */

/* ✅ Better */
.container { max-width: 1200px; width: 90%; }
```

## 🧪 Mini Practice Task

Create a page with:
- A full-screen hero (`100vh`) with centered text
- A container with `max-width: 1000px` centered on the page
- Three equally wide columns at `33.33%` each
- Font sizes using `rem` (h1: 3rem, h2: 2rem, p: 1rem)

## 📝 Homework

Build a "Pricing Page" with 3 pricing cards side-by-side. Each card must use:
- `%` for width
- `rem` for font sizes
- `px` for borders and small details
- `vh`/`vw` nowhere (practice when NOT to use them — pricing cards don't need it)

---

*Next up → [Module 06: Fonts & Text Properties](../module-06-fonts/lesson.md)*