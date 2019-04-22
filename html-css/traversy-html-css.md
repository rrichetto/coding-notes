# Forms
- To make the cursor focus on an input when you click the *label* of that input: set the label's `for` attribute and the input's `id` attribute to the same value.

- Within a form, a button with `type="reset"` will clear all input fields when clicked.

# Backgrounds and Borders
- If you want a transparent image/logo, use .png

# Alignment
- On your containers (`.container`)
, always use `max-width` instead of `width`. This helps with responsive design.

# Inline, Block, Inline-Block
- In order to center an image using `margin: auto`, you first need to set the `display` of the image to `display: block;`

- Remember that you cannot use `width` or `margin` on an inline element. A solution is to set it to `display: inline-block;` which allows you to use widths and margins.

# Visibility
- `display: none;` completely removes the element from the document.
- `visibility: hidden;` makes the element invisible, but it still takes up the original space.

# Sticky Navbar
- To make a navbar stick at the top, use:
```css
#navbar {
  position: sticky;
  top: 0;
  z-index: 1;
}
```

# Showcase Background Image
- To set an image that covers the whole screen, use `height: 100vh`;

- A common way to set a large background image for the header/showcase:
```css
#showcase {
  background: url('../img/showcase.jpg') no-repeat center center/cover;
}
```