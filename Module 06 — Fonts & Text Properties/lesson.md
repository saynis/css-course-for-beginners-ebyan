# Module 06 — Fonts & Text Properties

> **Section:** Beginner
> **Est. Time:** 3 hours
> **Goal:** Control how text looks — the typography of your website

---

## Why Typography Matters

Typography is one of the most visible parts of web design. Good typography makes content readable, trustworthy, and attractive. Bad typography makes users leave.

---

## Lesson 6.1 — `font-family`

Sets the typeface of your text. Always provide a **fallback list** — if the first font isn't available, the browser tries the next.

```css
body {
  font-family: 'Georgia', Times, serif;
}

p {
  font-family: 'Helvetica Neue', Arial, sans-serif;
}

code {
  font-family: 'Courier New', Courier, monospace;
}
```

### Font Stacks

| Type | Example Fonts | Best For |
|------|---------------|---------|
| `serif` | Georgia, Times New Roman | Articles, editorial content |
| `sans-serif` | Arial, Helvetica | UI, modern layouts |
| `monospace` | Courier New, Consolas | Code blocks |
| `cursive` | Comic Sans (avoid!) | Very specific decorative use |

> Always end your font stack with a **generic family** (`serif`, `sans-serif`, `monospace`) as the final fallback.

---

## Lesson 6.2 — `font-size`

```css
h1 { font-size: 48px; }   /* Pixels — fixed */
p  { font-size: 1rem; }   /* Root-relative — preferred */
small { font-size: 0.875rem; } /* 14px if root is 16px */
```

**Typography scale** — use a consistent size scale:

```css
html { font-size: 16px; }

h1 { font-size: 3rem; }    /* 48px */
h2 { font-size: 2.25rem; } /* 36px */
h3 { font-size: 1.75rem; } /* 28px */
h4 { font-size: 1.25rem; } /* 20px */
p  { font-size: 1rem; }    /* 16px */
small { font-size: 0.875rem; } /* 14px */
```

---

## Lesson 6.3 — `font-weight`

Controls how **bold** the text is.

```css
p { font-weight: 400; }     /* Normal */
strong { font-weight: 700; } /* Bold */
.light { font-weight: 300; } /* Light */
.black { font-weight: 900; } /* Extra bold */
```

| Value | Keyword | Common use |
|-------|---------|------------|
| 100 | Thin | Display text, high contrast |
| 300 | Light | Body text, airy feel |
| 400 | Normal | Default body text |
| 500 | Medium | Slightly emphasized |
| 600 | Semibold | Buttons, labels |
| 700 | Bold | Headings |
| 900 | Black | Hero headlines |

> Not all fonts support all weights. Google Fonts lets you choose which weights to load.

---

## Lesson 6.4 — `text-align`

Horizontal alignment of text inside its container.

```css
h1 { text-align: center; }
p  { text-align: left; }   /* Default */
.footer-text { text-align: right; }
.newspaper { text-align: justify; } /* Stretches text to fill width — use carefully */
```

---

## Lesson 6.5 — `text-decoration`

Adds or removes lines on text.

```css
a { text-decoration: none; }        /* Remove underline from links */
u { text-decoration: underline; }   /* Underline */
.strike { text-decoration: line-through; } /* Strikethrough for deleted items */
.fancy { text-decoration: overline; }
```

**Modern CSS — control the decoration style:**

```css
a {
  text-decoration: underline;
  text-decoration-color: blue;
  text-decoration-style: dotted; /* solid | dotted | dashed | wavy */
  text-underline-offset: 4px;   /* Space between text and underline */
}
```

---

## Lesson 6.6 — `letter-spacing`

Controls space between individual characters.

```css
.spread-out { letter-spacing: 0.1em; }  /* Wider */
.tight { letter-spacing: -0.02em; }     /* Tighter */
.label { letter-spacing: 0.15em; text-transform: uppercase; } /* Classic label look */
```

---

## Lesson 6.7 — `line-height`

Controls the space **between lines** of text. This is one of the most important properties for readability.

```css
/* No unit = multiplier of font-size (best practice) */
body { line-height: 1.6; }  /* 1.6 × font-size */
h1   { line-height: 1.1; }  /* Tighter for large headings */

/* With units — fixed */
p { line-height: 28px; }    /* Fixed — doesn't scale with font-size */
```

**Readability guidelines:**
- Body text: `1.5` to `1.7`
- Headings: `1.1` to `1.3`
- Large display text: `1.0` to `1.1`

---

## Lesson 6.8 — Other Useful Text Properties

```css
/* Uppercase / lowercase / capitalize */
.nav-link { text-transform: uppercase; }
.name { text-transform: capitalize; }

/* Font style */
em { font-style: italic; }
.normal-style { font-style: normal; }

/* Text color */
p { color: #333; }

/* Indent first line */
p { text-indent: 2em; }

/* Limit text to N lines and add "..." */
.truncate {
  overflow: hidden;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
}
```

---

## Lesson 6.9 — Google Fonts Integration

Google Fonts gives you free, professional typefaces.

**Step 1:** Visit [fonts.google.com](https://fonts.google.com)
**Step 2:** Pick a font, select the weights you need
**Step 3:** Copy the `<link>` tag and paste it in your HTML `<head>` — **before** your own CSS

```html
<!DOCTYPE html>
<html>
<head>
  <!-- Google Fonts FIRST -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;600;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">

  <!-- Your CSS after -->
  <link rel="stylesheet" href="style.css">
</head>
```

**Step 4:** Use in your CSS:

```css
body {
  font-family: 'Inter', sans-serif;
}

h1, h2, h3 {
  font-family: 'Playfair Display', serif;
}
```

### Popular Font Pairings

| Heading Font | Body Font | Vibe |
|--------------|-----------|------|
| Playfair Display | Lato | Elegant, editorial |
| Montserrat | Open Sans | Clean, modern |
| Oswald | Merriweather | Strong, readable |
| Raleway | Nunito | Soft, friendly |
| Space Grotesk | Source Sans 3 | Tech, startup |

---

## Complete Typography System Example

```css
/* =========================================
   TYPOGRAPHY SYSTEM
   ========================================= */

html { font-size: 16px; }

body {
  font-family: 'Inter', sans-serif;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.6;
  color: #2d3748;
}

h1, h2, h3, h4 {
  font-family: 'Playfair Display', serif;
  font-weight: 700;
  line-height: 1.2;
  color: #1a202c;
  margin-bottom: 0.75em;
}

h1 { font-size: 3rem; }
h2 { font-size: 2.25rem; }
h3 { font-size: 1.75rem; }
h4 { font-size: 1.25rem; }

p {
  margin-bottom: 1.25em;
  max-width: 65ch; /* Optimal reading width */
}

a {
  color: #3182ce;
  text-decoration: underline;
  text-underline-offset: 3px;
}

.label {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: #718096;
}
```

---

## ⚠️ Important Notes

- Load Google Fonts **before** your own CSS to avoid invisible text flashing
- Don't load too many font weights — each adds page load time (1–3 weights per font is ideal)
- `max-width: 65ch` on paragraphs keeps lines at a comfortable reading width

## ❌ Common Beginner Mistakes

```css
/* ❌ No fallback font */
body { font-family: 'Roboto'; }

/* ✅ Always have fallbacks */
body { font-family: 'Roboto', Arial, sans-serif; }
```

```css
/* ❌ Using px for line-height — doesn't scale */
p { line-height: 24px; }

/* ✅ Use a unitless multiplier */
p { line-height: 1.6; }
```

## 🧪 Mini Practice Task

Create a blog post page with a proper typography system:
- Two Google Fonts: one for headings, one for body
- Consistent heading scale (h1 through h3) using rem
- Line height of 1.6 for paragraphs
- A `.caption` class with small, uppercase, letter-spaced text
- All link underlines removed, but a color change on hover

## 📝 Homework Assignment

Design a "Magazine Article" page. Requirements:
- Choose a sophisticated Google Font pairing
- Implement a full 6-level heading scale (h1–h6)
- Body text must be highly readable (right size, line-height, max-width)
- Include a blockquote styled with a left border and italic text
- A `.byline` style with the author's name (small, bold, spaced letters)

---

*Next up → [Module 07: CSS Box Model](../module-07-box-model/lesson.md)*