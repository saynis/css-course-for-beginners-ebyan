# Module 10 — Understanding CSS Specificity

> **Section:** Beginner
> **Est. Time:** 2 hours
> **Goal:** Understand why some CSS rules "win" over others

---

## The Cascading in CSS

CSS stands for **Cascading** Style Sheets. "Cascading" means there are rules for which style wins when multiple rules conflict.

This is **specificity** — a scoring system that determines which rule takes priority.

---

## Lesson 10.1 — Specificity Rules

When two rules target the same element and same property, specificity determines the winner.

**The rule:** More specific selector = higher priority.

---

## Lesson 10.2 — Specificity Score

Think of specificity as a 3-digit score: **(IDs, Classes, Elements)**

| Selector | IDs | Classes | Elements | Total |
|----------|-----|---------|----------|-------|
| `p` | 0 | 0 | 1 | 0-0-1 |
| `.card` | 0 | 1 | 0 | 0-1-0 |
| `p.card` | 0 | 1 | 1 | 0-1-1 |
| `#header` | 1 | 0 | 0 | 1-0-0 |
| `#header .nav a` | 1 | 1 | 1 | 1-1-1 |
| `div .card > p` | 0 | 1 | 2 | 0-1-2 |

Higher score = wins.

```css
/* Specificity 0-0-1 */
p { color: blue; }

/* Specificity 0-1-0 — WINS over element selector */
.intro { color: red; }

/* Both target: <p class="intro"> — .intro wins, text is red */
```

---

### Visualizing Specificity

```
                          ID    Class   Element
                          |       |       |
#header .nav a         =  1       1       1   →  1-1-1
.card .btn             =  0       2       0   →  0-2-0
div p                  =  0       0       2   →  0-0-2
```

---

## Lesson 10.3 — Specificity Examples

```css
/* 0-0-1: one element selector */
h2 {
  color: black;
}

/* 0-1-0: one class selector — WINS */
.title {
  color: blue;
}

/* 0-1-1: class + element */
h2.title {
  color: green; /* WINS over just .title */
}

/* 1-0-0: ID — WINS over everything above */
#page-title {
  color: red;
}
```

Given: `<h2 class="title" id="page-title">Hello</h2>`

Text color = **red** (ID wins with score 1-0-0).

---

## Lesson 10.4 — `!important`

`!important` **overrides all specificity**. It's a nuclear option.

```css
p { color: blue !important; }

/* Even an ID can't override !important */
#content p { color: red; } /* LOSES */

/* p is blue */
```

### When to use `!important`

Almost **never** in your own code. It's a sign of specificity problems.

**Legitimate uses:**
- Overriding a third-party library's styles (like Bootstrap)
- Utility classes meant to always win: `.hidden { display: none !important; }`

---



## ⚠️ Important Notes

- Inline styles (`style="..."`) have the highest specificity (almost like an ID) — another reason to avoid them
- `:not()`, `:is()`, `:where()` have different specificity behaviors
- The `*` universal selector has 0 specificity (0-0-0)

## ❌ Common Beginner Mistakes

```css
/* ❌ Adding more selectors to try to override a style */
div.container section.content article p {
  color: red; /* high specificity nightmare */
}

/* ✅ Write simple, specific class-based selectors */
.article-body { color: red; }
```

```css
/* ❌ Using !important to fight specificity wars */
p { color: blue !important; }
.note { color: green !important; }  /* Now you need !important everywhere */

/* ✅ Restructure your selectors instead */
```



## 📝 Homework Assignment

Take your homework from Module 2 (Team Members page) and:
1. Add an `id` to one team card and style it differently
2. Try to override that ID style using a class selector only — what happens?
3. Write a comment explaining why your override did or didn't work
4. Refactor all your CSS to use class selectors only (no IDs for styling)
5. Add a `.hidden` utility class with `display: none !important;` and explain in a comment why `!important` is acceptable here

---

*🎉 Beginner Section Complete! → [Module 11: CSS3 Visual Effects](../../02-advanced/module-11-visual-effects/lesson.md)*