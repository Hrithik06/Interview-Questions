# 1. In css which pseudo element targets first line of a block?
The CSS pseudo-element that targets the first line of a block is **`::first-line`** (or `:first-line` for backward compatibility).

- **Usage:**  
  ```css
  p::first-line {
    /* CSS properties */
    color: blue;
    font-weight: bold;
  }
  ```
- **Effect:**  
  Styles only the first formatted line of a block-level element, such as a `<p>` or `<div>`.
- **Notes:**  
  - The length of the first line depends on factors like the element’s width and font size.
  - Only certain CSS properties can be applied to `::first-line`.

**In summary:**  
Use the `::first-line` pseudo-element to target and style the first line of a block container in CSS.



# 2. Filters in CSS

The **CSS filter property** allows you to apply graphical effects to elements, such as images, backgrounds, and borders, directly in the browser—no image editing software required. Filters can adjust or transform the appearance of elements by blurring, changing brightness, adding shadows, and more.

---

### **Common CSS Filter Functions**

| Filter Function     | Description                                              | Example Usage                |
|---------------------|---------------------------------------------------------|------------------------------|
| `blur()`           | Softens the image by blurring its edges                  | `filter: blur(5px);`         |
| `brightness()`     | Adjusts the brightness (lighter/darker)                  | `filter: brightness(0.5);`   |
| `contrast()`       | Changes the contrast (difference between light/dark)     | `filter: contrast(200%);`    |
| `drop-shadow()`    | Adds a shadow behind the element                         | `filter: drop-shadow(2px 4px 6px black);` |
| `grayscale()`      | Converts the element to grayscale                        | `filter: grayscale(80%);`    |
| `hue-rotate()`     | Rotates the color hues                                   | `filter: hue-rotate(90deg);` |
| `invert()`         | Inverts the colors (like a photo negative)               | `filter: invert(100%);`      |
| `opacity()`        | Adjusts the transparency                                 | `filter: opacity(50%);`      |
| `saturate()`       | Changes color intensity                                  | `filter: saturate(150%);`    |
| `sepia()`          | Applies a warm, brownish tone (vintage effect)           | `filter: sepia(60%);`        |
| `url()`            | Applies an SVG filter via a URL                          | `filter: url('filters.svg#filter-id');` |

---

### **Syntax**

```css
/* Single filter */
img {
  filter: grayscale(100%);
}

/* Multiple filters */
img {
  filter: grayscale(30%) blur(3px) contrast(150%);
}
```
- Multiple filters are separated by spaces and applied in order, left to right.

---

### **Key Points**

- Filters can be applied to any HTML element, but are most commonly used on images and backgrounds.
- You can combine several filters for complex effects.
- The `filter` property is supported in all modern browsers.

---

**In summary:**  
CSS filters let you apply visual effects like blur, brightness, grayscale, and more to elements using the `filter` property and its functions, enabling dynamic and creative styling directly in your CSS.

# 3. How to give shadow to text?
To give shadow to text in CSS, use the `text-shadow` property. This property allows you to specify the horizontal and vertical offset, blur radius, and color of the shadow. Here’s the basic syntax:

```css
selector {
  text-shadow: <offset-x> <offset-y> <blur-radius> <color>;
}
```

**Example:**
```css
h1 {
  text-shadow: 2px 2px 5px red;
}
```
- `2px` is the horizontal shadow distance (to the right).
- `2px` is the vertical shadow distance (downward).
- `5px` is the blur radius (optional; makes the shadow softer).
- `red` is the shadow color.

You can also add multiple shadows by separating them with commas:

```css
h1 {
  text-shadow: 1px 1px 2px black, 0 0 25px blue, 0 0 5px darkblue;
}
```
This creates layered shadow effects.

**In summary:**  
Use the `text-shadow` property to add shadow effects to text, customizing the offset, blur, and color as desired.


# 4. What is a CSS Variable?How to Create a CSS Variable

A **CSS variable** (also called a custom property) is a user-defined value that can be reused throughout a stylesheet. CSS variables make your code more efficient, maintainable, and consistent by allowing you to define a value once and reference it in multiple places using the `var()` function. They are especially useful for managing colors, sizes, fonts, and other recurring values in large or complex stylesheets.

---

## How to Create a CSS Variable

### **1. Syntax for Defining a CSS Variable**

- CSS variable names must start with two dashes (`--`).
- They are defined inside a CSS selector's declaration block.

**Example:**
```css
:root {
  --main-bg-color: lightblue;
  --main-text-color: darkblue;
}
```
- The `:root` selector defines variables globally, making them accessible throughout the entire document.
- You can also define variables locally within any selector; these will only apply to that selector.

### **2. Using a CSS Variable**

- Reference a variable using the `var()` function:

```css
body {
  background-color: var(--main-bg-color);
  color: var(--main-text-color);
}
```
- The `var()` function can also take a fallback value: `var(--main-bg-color, white)`.

---

### **Summary Table**

| Step         | What to Do                                      | Example                              |
|--------------|-------------------------------------------------|--------------------------------------|
| Define       | Use `--name: value;` in a selector              | `:root { --primary: #3498db; }`      |
| Use          | Reference with `var(--name)`                    | `color: var(--primary);`             |
| Fallback     | Optional default: `var(--name, fallback)`       | `color: var(--primary, black);`      |

---

**In summary:**  
A CSS variable is a reusable, user-defined value set with a `--` prefix and used with the `var()` function. Define it in a selector (commonly `:root` for global scope), and use it anywhere in your CSS for cleaner, more maintainable code.

# 5. Position which allows elemnt to stay in place while scrolling?
The CSS position that allows an element to stay in place while scrolling is **`position: fixed;`**. When you use `position: fixed`, the element is positioned relative to the browser viewport, so it remains visible in the same spot even as you scroll the page. This is commonly used for sticky headers, navigation menus, or notification banners that should always be accessible regardless of scrolling.

**Example:**
```css
.fixed-element {
  position: fixed;
  top: 0;
  right: 0;
  /* other styles */
}
```

# 6. Sticky position

## What is `position: sticky` in CSS?

**`position: sticky`** is a CSS positioning property that allows an element to behave like a relatively positioned element until it reaches a specified threshold (such as `top`, `left`, `right`, or `bottom`) while scrolling. Once that threshold is crossed, the element "sticks" in place, behaving like a fixed element, but only within the boundaries of its parent container.

---

### **How Does It Work?**

- Initially, the element scrolls with the page (like `position: relative`).
- When the element reaches the specified offset (e.g., `top: 0`), it becomes fixed in that position as the user continues to scroll.
- The element remains "stuck" until its parent container is out of view; then it scrolls away with the parent.

---

### **Example Usage**

```css
.sticky-header {
  position: sticky;
  top: 0; /* The element will stick to the top of the viewport */
  background: #fff;
  z-index: 10;
}
```

---

### **Key Points**

- **Requires an Offset:** You must specify at least one offset property (`top`, `bottom`, `left`, or `right`) for `sticky` to work.
- **Contained by Parent:** The sticky behavior only works within the scrolling area of the parent element. If the parent scrolls out of view, the sticky element goes with it.
- **Use Cases:** Sticky navigation bars, table headers, sidebars, or banners that should remain visible while scrolling within a section.
- **Browser Support:** Supported in all major browsers except older Internet Explorer and Edge versions.

---

### **Comparison: `sticky` vs. `fixed`**

| Property           | `position: sticky`                                         | `position: fixed`                    |
|--------------------|-----------------------------------------------------------|--------------------------------------|
| Scroll Behavior    | Sticks at a threshold, within parent container            | Always fixed to viewport             |
| Initial State      | Relative                                                  | Fixed                                |
| Parent Boundaries  | Yes, sticky only inside parent                            | No, always visible                   |
| Use Case           | Section headers, sidebars, banners                        | Persistent navbars, floating buttons |

---

**In summary:**  
`position: sticky` lets an element scroll with its container until it reaches a specified offset, then "sticks" in place—ideal for headers, menus, or sidebars that should only remain visible within a section or container.

# 7. CSS value that makes an element invisible but still occupies space?
The CSS value that makes an element invisible but still occupies space is **`visibility: hidden`**.

- When you set `visibility: hidden` on an element, it becomes invisible to the user, but its allocated space in the layout remains unchanged.
- This is different from `display: none`, which removes the element entirely from the layout, causing other elements to shift as if it doesn’t exist.
- Example:
  ```css
  .invisible {
    visibility: hidden;
  }
  ```

**In summary:**  
Use `visibility: hidden` to hide an element while keeping its space in the page layout.

# 8. Width unit relative to viewport?

The CSS unit used to set an element’s width relative to the viewport is **`vw` (viewport width)**.  
- `1vw` equals 1% of the width of the viewport (the visible area of the browser window).
- For example, `width: 50vw;` will make the element’s width 50% of the viewport’s width, regardless of its parent container’s size.

Other related viewport units include:
- **`vh`**: 1% of the viewport’s height.
- **`vmin`**: 1% of the smaller dimension (width or height) of the viewport.
- **`vmax`**: 1% of the larger dimension (width or height) of the viewport.

**Example:**
```css
.box {
  width: 80vw; /* 80% of the viewport width */
}
```



# 9. CSS Media Query Syntax

A **CSS media query** allows you to apply styles conditionally based on device characteristics such as screen width, height, orientation, resolution, and more. Media queries are essential for responsive web design.

---

### **Basic Syntax**

```css
@media media-type and (media-feature) {
  /* CSS rules go here */
}
```css
- **media-type**: (optional) The type of device to target, such as `screen`, `print`, or `all` (default).
- **media-feature**: A condition to test, such as `(max-width: 600px)`.

---

### **Examples**

**1. Target screens with a maximum width of 600px:**
```css
@media (max-width: 600px) {
  body {
    background-color: #87ceeb;
  }
}
```
This applies the background color only when the viewport is 600px wide or less.

**2. Combine multiple conditions:**
```css
@media screen and (min-width: 600px) and (orientation: landscape) {
  body {
    color: blue;
  }
}
```
This applies styles only on screens that are at least 600px wide and in landscape orientation.

**3. Multiple queries (OR logic):**
```css
@media screen and (min-width: 600px), screen and (orientation: landscape) {
  body {
    color: blue;
  }
}
```
Styles apply if **either** condition is true.

**4. Negate a query:**
```css
@media not (orientation: landscape) {
  body {
    color: blue;
  }
}
```
Applies styles only when the device is **not** in landscape orientation.

---

### **Summary Table**

| Part             | Example                         | Description                                  |
|------------------|---------------------------------|----------------------------------------------|
| Media type       | `screen`, `print`, `all`        | Device type (optional)                       |
| Media feature    | `(max-width: 600px)`            | Condition to test                            |
| Logical operator | `and`, `not`, `,` (comma for OR)| Combine or negate conditions                 |

---

**In summary:**  
The CSS media query syntax uses the `@media` rule with optional media types and one or more media features, allowing you to apply styles based on device or environment characteristics.


# 10. CSS property used to add space **inside** an element’s border
The CSS property used to add space **inside** an element’s border (between the border and the element’s content) is **`padding`**.

- `padding` creates space on the inside of the border, ensuring the content does not touch the border.
- Example:
  ```css
  .box {
    padding: 20px;
  }
  ```
  This adds 20px of space on all sides between the border and the content.

**Note:**  
- `border-spacing` is used for spacing between table cells, not for spacing inside an element’s border.
- To add space outside the border, use `margin`.  
- To add space inside the border, use `padding`.

