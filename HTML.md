
# 1. In HTML which tag is used to embed external content, web page? iframe? embed?
Embedding External Content or Web Pages in HTML

## `<iframe>`

- The `<iframe>` tag is the standard and most commonly used element to embed an external web page or HTML content within your current document.
- It creates an inline frame that displays the content of the specified URL.

**Example:**

```html
 <iframe src="https://example.com" width="600" height="400"></iframe>
 ``` 


---

## `<embed>`

- The `<embed>` tag is mainly used to embed external resources like PDFs, multimedia files, or plugins.
- It is less commonly used for embedding full web pages.
- Has fewer attributes and less flexibility compared to ``.

---

## `<object>`

- The `<object>` tag can also embed external resources, including HTML pages.
- It is more versatile but less commonly used today for embedding web pages.
- Has different behavior and compatibility considerations.

---

## Summary

| Tag       | Use Case                                     | Notes                                  |
|-----------|----------------------------------------------|----------------------------------------|
| `<iframe>` | Embed external web pages or HTML documents  | Standard, widely supported             |
| `<embed>`  | Embed multimedia, PDFs, plugins              | Less common for web pages              |
| `<object>` | Embed various external resources including HTML | Versatile but less common for pages |

---

**In brief:**  
Use the `<iframe>` tag to embed external web pages in HTML. It provides the best support and flexibility for this purpose.

# 2. HTML attribute to make sure form field is filled?

## HTML Attribute to Ensure a Form Field is Filled

The HTML attribute used to make sure a form field is filled before submitting the form is **`required`**.

- The `required` attribute is a boolean attribute.
- When present on an input, select, or textarea element, it ensures that the field must be filled out before the form can be submitted.
- If the field is left empty, the browser will prevent form submission and typically display a validation error message.

**Example:**
```html
 <input type="text" name="username" required> 
```

**Supported Elements:**  
Works with various input types (text, email, password, checkbox, radio, etc.), as well as `<select>` and `<textarea>`.

**Summary:**  
Use the `required` attribute to ensure a form field must be filled before submission.

# 3. Tag which divides content aside from page content such as sidebar?
The HTML tag used to divide content aside from the main page content—such as a sidebar—is the **`<aside>`** tag.

- The `<aside>` tag is specifically designed to mark up content that is tangentially or indirectly related to the main content, such as sidebars, pull quotes, or groups of related links.
- It is commonly used for sidebars that contain menus, widgets, related articles, or other supplementary information.
- While `<aside>` is semantically appropriate for sidebars, the visual appearance as a sidebar is achieved with CSS.

**Example:**
```html
<aside>
  <!-- Sidebar content such as menus, widgets, or related links -->
</aside>
```

**In summary:**  
Use the `<aside>` tag to semantically define a sidebar or any content that is separate from, but related to, the main page content.



# 4. HTML Tag to set a Horizontal Rule

The HTML tag used to create a horizontal rule (a horizontal line) that visually separates content or defines a thematic break is the **``** tag.

- It is a self-closing (void) element and does not require a closing tag.
- By default, it renders as a horizontal line across the width of its container.
- Semantically, `<hr>` represents a thematic break between sections of content.
- It supports attributes like `width`, `size` (height), `color`, and `align` (though some are deprecated and styling is better done with CSS).

### Basic Example:
```html
 <p>Section before the line.</p> <hr> <p>Section after the line.</p>
``` 

### Customizing with CSS:
```html
hr {
  border: none;
  border-top: 2px solid #0000ff; /* blue horizontal line */
  width: 50%;                    /* half the container width */
  margin: 20px auto;             /* centered with vertical spacing */
}
```

---

**Summary:**  
Use the `<hr>` tag to insert a horizontal rule in HTML, which creates a visual and semantic separation between content sections.

# 5. Input type for select file?

## Input Type for Selecting a File in HTML

To allow users to select a file for upload in an HTML form, use the following input type:

```html
<input type="file">
```

- This creates a file-select field with a "Browse" button, enabling users to choose one or more files from their device.
- To allow multiple file selection, add the `multiple` attribute:

  ```
  <input type="file" multiple>
  ```

- You can further restrict selectable file types using the `accept` attribute (e.g., `accept="image/*"` for images).

**Example:**
```html
<form>
  <label for="myfile">Select a file:</label>
  <input type="file" id="myfile" name="myfile">
</form>
```

**Summary:**  
Use `<input type="file">` to let users select and upload files in HTML forms.
# 6. HTML Tag to set a Line break
The HTML tag used to set a line break is **`<br>`**.

- The `` tag inserts a single line break in text, starting the following content on a new line.
- It is an empty (void) tag, so it does not require a closing tag.
- Commonly used in poems, addresses, or anywhere you need to force a new line within text without starting a new paragraph.

**Example:**
```html
<p>This is the first line.<br>This is the second line.</p>
```

**Summary:**  
Use the `<br>` tag wherever you want to insert a line break in HTML.

# 7. Prevent form field from being edited
To prevent a form field from being edited in HTML, use the **`readonly`** attribute on the input or textarea element. This makes the field non-editable, but users can still focus, highlight, and copy its content. The value of a readonly field will be included when the form is submitted.

**Example:**
```html
<input type="text" value="This field cannot be edited" readonly>
<textarea readonly>This text area is read-only.</textarea>
```

**Key points:**
- `readonly` works with input types like text, email, number, password, and textarea.
- It does **not** apply to select, checkbox, radio, file, or button elements.
- The field remains focusable and its value is sent with the form on submission.
- Use `disabled` if you want the field to be both non-editable and excluded from form submission.

**Summary:**  
Add the `readonly` attribute to an input or textarea to prevent editing while still submitting its value with the form.

