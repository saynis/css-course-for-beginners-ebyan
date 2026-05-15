# Module 09 — CSS Overflow

> **Section:** Beginner
> **Est. Time:** 1 hour
> **Goal:** Control what happens when content is too big for its container

---

## What is Overflow?

When content is larger than its container, it **overflows**. CSS lets you control what happens in that situation.

---

## Lesson 9.1 — `overflow` Values

### `overflow: visible` (Default)

Content spills out of the container without clipping. The container doesn't grow.

```css
.box {
  width: 200px;
  height: 100px;
  overflow: visible;
  border: 2px solid red;
}
/* Text will spill OUTSIDE the red border */
```

---

### `overflow: hidden`

Content that goes beyond the container is **cut off** (clipped). Nothing scrolls.

```css
.card {
  width: 300px;
  height: 200px;
  overflow: hidden;  /* Clips any content that overflows */
}


```

---

### `overflow: scroll`

**Always** shows scrollbars, even if content fits.

```css
.box {
  overflow: scroll; /* Scrollbars always visible — often ugly */
}
```

---

### `overflow: auto` ✅ (Recommended)

Scrollbars appear **only when needed**. This is what you want most of the time.

```css
.chat-window {
  height: 400px;
  overflow: auto;  /* Scroll only when messages overflow */
}

.code-block {
  overflow: auto;  /* Horizontal scroll for long code lines */
}
```

---

## Lesson 9.2 — `overflow-x` and `overflow-y`

Control overflow on each axis independently.

```css
/* Scroll horizontally, hide vertically */
.table-wrapper {
  overflow-x: auto;
  overflow-y: hidden;
}

/* Scroll vertically (like a sidebar), hide horizontal */
.sidebar {
  height: 100vh;
  overflow-y: auto;
  overflow-x: hidden;
}
```

---


## ⚠️ Important Notes

- `overflow: hidden` is often used to "contain" floated children (alternative to clearfix)
- `overflow: hidden` on a parent clips `position: absolute` children — sometimes unexpected





## 📝 Homework

Build a "Chat App" layout:
- A fixed sidebar (full height, scrollable if many contacts)
- A main chat area that scrolls vertically
- A message input fixed at the bottom
- Messages that overflow the chat window should scroll, not spill

---

*Next up → [Module 10: Understanding Specificity](../module-10-specificity/lesson.md)*