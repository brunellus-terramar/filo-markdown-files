# HTML in Markdown

This document tests various HTML elements embedded within Markdown content.

## Basic HTML Tags

### Inline HTML

This paragraph contains <strong>bold via HTML</strong> and <em>italic via HTML</em> text.

You can also use <code>inline code</code> with HTML tags.

Here's a <mark>highlighted</mark> word using the mark tag.

### Line Breaks

Line one<br>Line two<br>Line three

### Horizontal Rules

Above the rule
<hr>
Below the rule

## Block-Level HTML

### Divs with Styling

<div style="background-color: #f0f0f0; padding: 10px; border-radius: 5px;">
This is a styled div block with a gray background.
</div>

### Details/Summary (Collapsible)

<details>
<summary>Click to expand</summary>

This content is hidden by default and reveals when you click the summary.

- Item 1
- Item 2
- Item 3

</details>

<details open>
<summary>Already expanded</summary>

This details block starts open.

</details>

## Tables with HTML

### Pure HTML Table

<table>
  <thead>
    <tr>
      <th>Header 1</th>
      <th>Header 2</th>
      <th>Header 3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Row 1, Cell 1</td>
      <td>Row 1, Cell 2</td>
      <td>Row 1, Cell 3</td>
    </tr>
    <tr>
      <td>Row 2, Cell 1</td>
      <td>Row 2, Cell 2</td>
      <td>Row 2, Cell 3</td>
    </tr>
  </tbody>
</table>

### Table with Colspan/Rowspan

<table border="1">
  <tr>
    <th colspan="2">Merged Header</th>
  </tr>
  <tr>
    <td rowspan="2">Spans 2 rows</td>
    <td>Cell A</td>
  </tr>
  <tr>
    <td>Cell B</td>
  </tr>
</table>

## Mixed Markdown and HTML

### Markdown Inside HTML

<div>

**This bold text** uses Markdown syntax inside a div.

- List item 1
- List item 2

</div>

### HTML Inside Markdown Lists

- Regular list item
- <span style="color: blue;">Blue colored item</span>
- Another regular item

### Nested Structures

<blockquote>
<p>This is an HTML blockquote with a <strong>bold</strong> word.</p>
<p>It has multiple paragraphs.</p>
</blockquote>

## Special HTML Elements

### Superscript and Subscript

Water is H<sub>2</sub>O.

Einstein's equation: E = mc<sup>2</sup>

### Keyboard Input

Press <kbd>Ctrl</kbd> + <kbd>C</kbd> to copy.

### Abbreviations

<abbr title="HyperText Markup Language">HTML</abbr> is the standard markup language.

### Definition Lists

<dl>
  <dt>Term 1</dt>
  <dd>Definition for term 1</dd>
  <dt>Term 2</dt>
  <dd>Definition for term 2</dd>
</dl>

## Image with HTML

<figure>
  <img src="https://via.placeholder.com/150" alt="Placeholder image">
  <figcaption>Figure 1: A placeholder image</figcaption>
</figure>

## Forms (Display Only)

<form>
  <label for="name">Name:</label>
  <input type="text" id="name" name="name" placeholder="Enter your name" disabled>
  <br><br>
  <label for="email">Email:</label>
  <input type="email" id="email" name="email" placeholder="Enter your email" disabled>
</form>

## Comments

<!-- This is an HTML comment and should not be visible -->

The comment above should not render.

## Escaped HTML

These should show as literal text:
- `<div>` (code block)
- &lt;span&gt; (HTML entities)

## Edge Cases

### Empty Tags

<div></div>
<span></span>

### Self-Closing Tags

<img src="" alt="empty image"><br>
<input type="text" disabled>

### Malformed HTML (Browser should handle gracefully)

<div>Unclosed div

<p>Paragraph without closing

---

## Test Results Checklist

- [ ] Inline HTML tags render correctly (strong, em, code, mark)
- [ ] Line breaks work with br tags
- [ ] Block-level divs render with styles
- [ ] Details/summary elements are collapsible
- [ ] HTML tables render properly
- [ ] Colspan/rowspan work in tables
- [ ] Markdown works inside HTML blocks
- [ ] Superscript/subscript display correctly
- [ ] kbd tags style as keyboard keys
- [ ] HTML comments are hidden
- [ ] Escaped HTML shows as literal text
