# Module 15 — Media Queries & Responsive Design

> **Section:** Advanced
> **Est. Time:** 4 hours
> **Goal:** Make your websites look great on every screen size

---

## What Is Responsive Design?

Responsive design means your website **adapts** to different screen sizes — phones, tablets, laptops, desktops, and TVs. One codebase, every device.

Before responsive design, developers built entirely separate mobile websites (m.example.com). Today, CSS handles it all elegantly.

### Real-World Analogy

Think of a responsive website like **water** — it takes the shape of whatever container it's in. A glass, a bottle, a bowl — the water adjusts. Your layout should do the same.

---

## Lesson 15.1 — The Viewport Meta Tag

**This is the first and most critical step.** Add this to every HTML page's `<head>` — without it, nothing else works on mobile.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

Without this tag, mobile browsers zoom out to display the "desktop" version of your page, making everything tiny. This tag tells the browser: "Use the actual device width as the page width."

---

## Lesson 15.2 — Media Queries

A media query is a conditional block of CSS — it **only applies when a condition is true**, such as the screen being a certain width.

```css
/* Syntax */
@media (condition) {
  /* CSS rules that apply only when condition is met */
}
```

### Width-Based Queries

```css
/* Applies when screen is 768px wide or LESS */
@media (max-width: 768px) {
  .sidebar {
    display: none;
  }
}

/* Applies when screen is 1024px wide or MORE */
@media (min-width: 1024px) {
  .container {
    max-width: 1200px;
  }
}

/* Applies BETWEEN two widths */
@media (min-width: 768px) and (max-width: 1199px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

---

## Lesson 15.3 — Breakpoints

Breakpoints are the screen widths at which your layout changes. Here are the most commonly used ones:

```css
/* Extra small — small phones */
@media (max-width: 480px) { }

/* Small — phones (most common) */
@media (max-width: 768px) { }

/* Medium — tablets */
@media (max-width: 1024px) { }

/* Large — small laptops */
@media (max-width: 1280px) { }

/* Extra large — big desktops */
@media (min-width: 1440px) { }
```

> **Important:** These are guidelines, not laws. Your breakpoints should be determined by where your *content* starts to look bad — not by specific device names.

---

## Lesson 15.4 — Mobile-First Design ✅ (The Right Way)

There are two approaches to writing responsive CSS:

### ❌ Desktop-First (Older Approach)

Write full desktop styles, then use `max-width` queries to override them for smaller screens.

```css
/* Desktop styles written first */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 32px;
}

/* Then strip down for mobile */
@media (max-width: 768px) {
  .grid {
    grid-template-columns: 1fr;
    gap: 16px;
  }
}
```

### ✅ Mobile-First (Modern, Recommended)

Write the **simplest mobile styles first**, then use `min-width` queries to *add* complexity as the screen gets larger.

```css
/* Mobile styles — simple, single column */
.grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

/* Tablet — two columns */
@media (min-width: 600px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 24px;
  }
}

/* Desktop — three columns */
@media (min-width: 1024px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 32px;
  }
}
```

**Why mobile-first wins:**
- Mobile is the majority of web traffic worldwide
- Forces you to prioritize essential content
- Cleaner, more maintainable CSS
- Adds complexity only where needed — mobile gets the lightest CSS

---

## Lesson 15.5 — Responsive Layouts in Practice

### Responsive Navigation

```html
<nav class="navbar">
  <div class="nav-logo">Brand</div>
  <button class="hamburger" id="hamburger">☰</button>
  <ul class="nav-links" id="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Work</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

```css
/* ---- MOBILE FIRST ---- */
.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 16px 24px;
  background: white;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-logo {
  font-size: 1.25rem;
  font-weight: 700;
  color: #1a202c;
}

/* Hamburger visible on mobile */
.hamburger {
  display: block;
  background: none;
  border: 1px solid #e2e8f0;
  border-radius: 6px;
  padding: 6px 10px;
  font-size: 1.2rem;
  cursor: pointer;
}

/* Nav links hidden on mobile by default */
.nav-links {
  display: none;
  list-style: none;
  flex-direction: column;
  gap: 8px;
  position: absolute;
  top: 61px;
  left: 0;
  right: 0;
  background: white;
  padding: 16px 24px 24px;
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.1);
}

/* When JS adds .open class */
.nav-links.open {
  display: flex;
}

.nav-links a {
  color: #4a5568;
  text-decoration: none;
  font-weight: 500;
  padding: 8px 0;
  border-bottom: 1px solid #f0f0f0;
}

/* ---- DESKTOP 768px+ ---- */
@media (min-width: 768px) {
  .hamburger {
    display: none; /* Hide hamburger */
  }

  .nav-links {
    display: flex !important; /* Always show links */
    flex-direction: row;
    gap: 32px;
    position: static;
    box-shadow: none;
    padding: 0;
  }

  .nav-links a {
    border-bottom: none;
    padding: 0;
  }
}
```

---

### Responsive Card Grid

```css
/* Mobile — single column */
.cards-grid {
  display: grid;
  grid-template-columns: 1fr;
  gap: 20px;
  padding: 24px 16px;
}

/* Tablet — two columns */
@media (min-width: 600px) {
  .cards-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

/* Desktop — three columns */
@media (min-width: 1024px) {
  .cards-grid {
    grid-template-columns: repeat(3, 1fr);
    gap: 32px;
    padding: 48px 0;
  }
}
```

**Even better — no media queries needed:**

```css
/* Automatically fits as many columns as possible,
   never smaller than 280px each */
.cards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}
```

---

### Responsive Typography

```css
/* Mobile */
h1 { font-size: 2rem; }
h2 { font-size: 1.5rem; }
p  { font-size: 1rem; }

/* Tablet */
@media (min-width: 768px) {
  h1 { font-size: 2.75rem; }
  h2 { font-size: 2rem; }
}

/* Desktop */
@media (min-width: 1024px) {
  h1 { font-size: 3.5rem; }
  h2 { font-size: 2.5rem; }
}
```

---

### Responsive Spacing

```css
.section {
  padding: 48px 16px; /* Mobile — tighter */
}

.container {
  width: 100%;
  padding: 0 16px;
  margin: 0 auto;
}

@media (min-width: 768px) {
  .section {
    padding: 64px 32px;
  }

  .container {
    padding: 0 32px;
  }
}

@media (min-width: 1024px) {
  .section {
    padding: 96px 0;
  }

  .container {
    max-width: 1200px;
    padding: 0 48px;
  }
}
```

---

### Responsive Images

```css
/* All images responsive by default */
img {
  max-width: 100%;
  height: auto;
  display: block;
}

/* Hero image that grows with screen */
.hero-image {
  width: 100%;
  height: 280px;
  object-fit: cover;
  object-position: center;
}

@media (min-width: 768px) {
  .hero-image { height: 420px; }
}

@media (min-width: 1024px) {
  .hero-image { height: 580px; }
}
```

---



## ⚠️ Important Notes

- Always include `<meta name="viewport">` — without it, responsive CSS won't work on real devices
- Test in Chrome DevTools (F12 → device toolbar icon) at 320px, 375px, 768px, and 1280px

---

## ❌ Common Beginner Mistakes

```html
<!-- ❌ Forgetting the viewport meta tag -->
<head>
  <title>My Site</title>
  <!-- No viewport tag — mobile will zoom out! -->
</head>

<!-- ✅ Always include it -->
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

---

## 🧪 Mini Practice Task

Take any page you built earlier in this course and make it fully responsive:

1. Add the viewport meta tag (if missing)
2. Rewrite the CSS mobile-first
3. Add breakpoints at `600px` and `1024px`
4. Make the navigation collapse to a hamburger on mobile
5. Make the card grid stack to one column on mobile

Test at: 320px, 480px, 768px, and 1280px.

---

## 📝 Homework Assignment

Build a **fully responsive Blog Page** from scratch, mobile-first:

**Mobile layout (< 768px):**
- Hamburger menu 
- Single-column article cards
- Full-width hero image
- Compact font sizes

**Tablet layout (768px – 1023px):**
- Horizontal nav links
- Two-column article grid
- Medium font sizes

**Desktop layout (1024px+):**
- Full navbar with logo, links, and CTA button
- Three-column article grid
- Large featured article spanning full width at top
- Right sidebar with categories

**Requirements checklist:**
- [ ] `<meta name="viewport">` present
- [ ] Mobile-first CSS (only `min-width` queries)
- [ ] Minimum 3 breakpoints
- [ ] Responsive images with `max-width: 100%`
- [ ] No horizontal scroll at any width
- [ ] Tested in DevTools at 320px, 768px, and 1280px

---

*🎓 Advanced Section Complete! Time to build projects →*