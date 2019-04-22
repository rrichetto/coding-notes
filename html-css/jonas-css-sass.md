[TOC]

# 7-1 Architecture with SASS

- This architecture is designed for larger, multi-page websites.
- 7 different folders for partial Sass files, and 1 main Sass file to import all other files into a complied CSS stylesheet.
- The Seven Folders:
  - base/
  - components/
  - layout/
  - pages/
  - themes/
  - abstracts/
  - vendors/
- Example:
  - `base` folder - basic project definitions, like a project boilerplate
    - `_base.scss` - for low-level basics and global definitions, like resets and styles for `html` and `body` element selectors
    - `_animations.scss`
    - `_typography.scss`
    - `_utilities.scss`
  - `abstract` folder - code that will not output any CSS, like variables, mixins, functions, etc.
    - `_variables.scss`
    - `_mixins.scss`
    - `_functions.scss`
  - `components` folder - reusable and independant blocks. Can be used anywhere.
    - `button.scss`
  - `layout` folder - global header, footer, etc. Should work on all pages.
    - `_header.scss`
  - `pages` - specific styles for a specific pages
    - `_home.scss`
  - `themes` folder - for a web app with different themes
  - `venders` folder - 3rd party CSS, like the file for Bootstrap or FontAwesome.



# background-size: … ;

```css
/* To fit an image entirely inside of an element */
element {
  background-size: cover;
}
```



# background-position: … ;

```css
/* When viewport is resized, top of image stays in place */
element {
  background-position: top; /* bottom, center */
}
```



# Background Image with a Gradient Overlay

```css
element {
  /* from frontmost to backmost image */
  background-image: linear-gradient(
    to right bottom,
    rgba(126, 213, 111, 0.8), 
    rgba(40, 180, 133, 0.8)),
    url('../img/hero.jpg');
}
```



# Image Positioning

- Since an image is a inline level element, it is often best to first place the image inside of a div container, and then position the container.



# Center a header text in middle of showcase/header

```css
.text-box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```



# There are two ways to animate a property

1. The simple way: `transform: … ;`
2. The detailed way: `@keyframes … { }` and `animation: … ;`



# The only 2 properties you should animate

- Due to browswer performance, you should only ever animate `opacity` and `transform`.
  - But remember that you can do a lot of things with `transform`.



# Animations - common properties

```css
element {
  animation-name: moveInLeft;
  animation-duration: 1s;
  animation-timing-function: ease-out;
  animation-delay: 3s;
  animation-iteration-count: 3;
  animation-fill-mode: forwards;

 
  /* Shorthand */
  /* name - duration - timing function */
  animation: moveInLeft 1s ease-out;
}

@keyframes moveInLeft {
  0% {
    transform: translateX(-100px);
  }
  
  100% {
    transform: translateX(0);
  }
}

```



# Formatting and Aligning a Button

- To position a button, it is often good to use `display: inline-block;`. This will treat it like text, which means you can use `text-align: center;`. But it is also treated like a block element.



# How to make a button look like it is being pressed down into the page

```css
/* the HTML element is an 'a' tag with class=".btn btn-white" */

.btn:link,
.btn:visited {
  text-transform: uppercase;
  text-decoration: none;
  padding: 15px 40px;
  display: inline-block;
  border-radius: 100px;
  transition: all .2s;
}

.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
}

.btn:active {
  transform: translateY(-1px);
  box-shadow: 0 5px 10px rgba(0, 0, 0, 0.2);
}

.btn-white {
  background-color: #fff;
  color: #777;
}
```



# The 3 Pillars of writing good, professional HTML and CSS

You must pay attention to all three:

1. Responsive Design
2. Maintainable and Scalable
3. Web Performance



	# The Difference between length and width percentages

- If used to specity `font-size`, percentages are relative to their parent's font-size.
- But if used to specity lengths (like in `padding` or `margin`), percentages are relative to their parent's `width`, **not** the font-size.



# A Better Reset

```css
*,
*::after,
*::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

body {
  box-sizing: border-box;
}
```



## Block, Inline, and Inline-Block Elements

**Block**

- Elements formatted as blocks
- Occupy 100% of parent's width
- Line breaks, align vertically
- Box model applies as usual



**Inline**

- Elements formated as lines
- Occupies only content's space
- No-line breaks
- *Only* horizontal paddings and margin (left and right)



**Inline-Block**

- Occupies only content's space (like Inline)
- No line-breaks (like Inline)
- Box model applies as usual - You can use vertical margin and padding (like Block)



# BEM - Block Element Modifier

- **Block** - a standalone component that is meaningful on its own
- **Element** - part of a block that has no standalone meaning
- **Modifier** - a different version of a block or an element





