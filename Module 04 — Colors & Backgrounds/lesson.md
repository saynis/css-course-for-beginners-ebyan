# Module 04 — Colors & Backgrounds

> **Section:** Beginner
> **Est. Time:** 3 hours
> **Goal:** Master every way to define colors and create beautiful backgrounds

---

## Lesson 4.1 — How Colors Work in CSS

CSS gives you several ways to define colors. Understanding all of them gives you more control and flexibility as a designer-developer.

---

## Lesson 4.2 — Hex Colors

Hex (hexadecimal) is the most common color format. It uses a `#` followed by 6 characters (0–9 and A–F).

```css
h1 { color: #ff0000; }  /* Red */
h2 { color: #00ff00; }  /* Green */
h3 { color: #0000ff; }  /* Blue */
p  { color: #333333; }  /* Dark gray */
```

### How Hex Works

Hex is split into three pairs: `#RRGGBB`

- `RR` = Red channel (00 to FF)
- `GG` = Green channel (00 to FF)
- `BB` = Blue channel (00 to FF)

`00` = none of that color, `FF` = full intensity

```css
/* Pure colors */
color: #ff0000; /* Full red, no green, no blue */
color: #ffffff; /* Full red + green + blue = white */
color: #000000; /* No red, no green, no blue = black */

/* Common useful hex values */
color: #f5f5f5; /* Light gray (great for backgrounds) */
color: #2c3e50; /* Dark blue-gray (great for text) */
color: #e74c3c; /* Nice red */
color: #3498db; /* Nice blue */
color: #2ecc71; /* Nice green */
```

### Shorthand Hex

When both characters in each pair are the same, you can shorten it:

```css
#ffffff → #fff
#000000 → #000
#ff0000 → #f00
#aabbcc → #abc
```

---

## Lesson 4.3 — RGB & RGBA

RGB uses **numbers 0–255** for each color channel. RGBA adds a 4th value for **opacity** (0 = invisible, 1 = fully visible).

```css
/* RGB */
color: rgb(255, 0, 0);       /* Red */
color: rgb(51, 51, 51);      /* Dark gray */
color: rgb(52, 152, 219);    /* Nice blue */

/* RGBA — 4th value is opacity */
color: rgba(255, 0, 0, 1);     /* Fully opaque red */
color: rgba(255, 0, 0, 0.5);   /* 50% transparent red */
color: rgba(255, 0, 0, 0);     /* Completely invisible */
```

### When to Use RGBA

```css
/* Semi-transparent dark overlay on images */
.overlay {
  background: rgba(0, 0, 0, 0.6); /* Black at 60% opacity */
}

/* Subtle shadow effect */
.card {
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
}

/* Muted background tint */
.highlight {
  background: rgba(52, 152, 219, 0.15); /* Light blue tint */
}
```

---


## Lesson 4.5 — Named Colors

CSS has 140+ named colors for convenience:

```css
color: red;
color: blue;
color: tomato;
color: coral;
color: steelblue;
color: mediumseagreen;
color: rebeccapurple;
```

Use these for quick tests, but use hex or HSL for real projects (more precision).

---

## Lesson 4.6 — Background Color

```css
body {
  background-color: #f0f4f8;
}

.card {
  background-color: white;
}

.hero {
  background-color: hsl(220, 90%, 15%);
}
```

**Shorthand:** You can use `background` instead of `background-color`:

```css
body { background: #f0f4f8; }
```

---

## Lesson 4.7 — Background Image

```css
.hero {
  background-image: url('images/hero.jpg');
}
```

The path in `url()` works like `href` in HTML — it's relative to your CSS file.

---

## Lesson 4.8 — Background Repeat

By default, background images **tile** (repeat) to fill the element. Control this with:

```css
.element {
  background-image: url('pattern.png');
  background-repeat: repeat;    /* Default: tiles in both directions */
  background-repeat: no-repeat; /* Shows image once only */
  background-repeat: repeat-x;  /* Tiles horizontally only */
  background-repeat: repeat-y;  /* Tiles vertically only */
}
```

For photos or illustrations, you almost always want `no-repeat`.

---

## Lesson 4.9 — Background Size

```css
.hero {
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  background-size: cover;    /* Fill the element, may crop the image */
  background-size: contain;  /* Fit the image fully, may leave empty space */
  background-size: 100% 50%; /* Exact width and height */
  background-size: 400px;    /* Specific pixel width */
}
```

`cover` is the most commonly used — it fills the container and looks great for hero sections.

---

## Lesson 4.10 — Background Position

Control where the image is anchored:

```css
.hero {
  background-position: center center; /* Default-ish */
  background-position: top left;
  background-position: bottom right;
  background-position: 50% 30%;  /* Horizontal% Vertical% */
  background-position: center;   /* Shorthand for center center */
}
```

---

## Lesson 4.11 — Combining Background Properties

You can write everything in one `background` shorthand:

```css
/* Long way */
.hero {
  background-color: #1a1a2e;
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}

/* Shorthand — one line */
.hero {
  background: #1a1a2e url('hero.jpg') no-repeat center / cover;
}
```

> **Pro tip:** The order in shorthand is: `color image repeat position / size`



## ⚠️ Important Notes

- `background-color` shows **through transparent areas** of a `background-image`
- `background-size: cover` may crop your image — make sure your subject is centered
- You can layer **multiple backgrounds** (advanced): `background: url('top.png'), url('bottom.jpg');`

---

## ❌ Common Beginner Mistakes

```css
/* ❌ Forgetting url() for background images */
background-image: 'photo.jpg'; /* Wrong! */

/* ✅ Correct */
background-image: url('photo.jpg');
```

```css
/* ❌ Forgetting background-repeat and the image tiles everywhere */
.hero {
  background-image: url('hero.jpg');
  /* Image will repeat! */
}

/* ✅ Always set repeat for full-image backgrounds */
.hero {
  background-image: url('hero.jpg');
  background-repeat: no-repeat;
  background-size: cover;
}
```

---

## 🧪 Mini Practice Task

Build a page with two sections:

**Section 1 — "Color Swatches"**
Create 5 `<div>` elements, each with a different background color using:
- A hex color
- An RGB color
- An RGBA color (with transparency)
- An HSL color
- A named color

Each div should be 100px × 100px with a label.

**Section 2 — "Hero Section"**
Create a hero section with:
- A background image (use any free image from [unsplash.com](https://unsplash.com))
- `background-size: cover` and `no-repeat`
- A semi-transparent dark overlay using RGBA
- White text centered over it

---

## 📝 Homework Assignment

**Build a "Travel Destination" landing page** with:

1. A full-screen hero section with a background image, overlay, and centered white text
2. A "featured destinations" section with 3 cards — each card has a different background color (use HSL for all three — just change the hue value)
3. A dark footer with a white text color
4. A color palette comment at the top of your CSS file documenting the 3–5 colors you used and their purpose

**Bonus:** Use RGBA to create a frosted-glass effect on the hero content box.

---

*Next up → [Module 05: Units & Dimensions](../module-05-units/lesson.md)*