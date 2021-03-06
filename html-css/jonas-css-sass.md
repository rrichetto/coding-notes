[TOC]

# 7-1 Architecture with SASS

- For an excellent breakdown/summary: <https://sass-guidelin.es/#the-7-1-pattern>
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
    - `_button.scss`
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



# Prevent a Transformed / Animated Element from Shuttering / Shaking

```css
element {
  transition: all .2s;
  backface-visibility: hidden;
}

element:hover {
  transform: scale(1.1);
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
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

body {
  box-sizing: border-box;
}
```



# Block, Inline, and Inline-Block Elements

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

- BEM relies on consistent, low-specificity selectors. This helps to avoid specificity issues in the cascade.
  - **Block** - a standalone component that is meaningful on its own
  - **Element** - part of a block that has no standalone meaning
  - **Modifier** - a different version of a block or an element

# BEM Naming

```html
<nav class='navigation'>
  <ul class='navigation__list'>
      <!-- When referring to grandchild elements, it is bem convention to prefix the class with the block element's name, rather than the direct parent (Element) name -->
      <li class='navigation__list-item'><a class='navigation__link' href="#">About Us</a></li>
      <li class='navigation__list-item'><a class='navigation__link' href="#">Pricing</a></li>
      <li class='navigation__list-item'><a class='navigation__link' href="#">Contact</a></li>
  </ul>
  <div class="navigation__buttons">
      <a href="#" class="navigation__btn navigation__btn--main">Sign Up</a>
      <a href="#" class="navigation__btn navigation__btn--hot">Get a quote</a>
  </div>
</nav>
```

# SASS: Functions - Lighten and Darken

```scss
element {
  background-color: red;
  
  &:hover {
    background-color: lighten(red, 15%);
    background-color: darken(red, 15%);
  }
}
```

# SASS: Creating Your Own Functions

```scss
@function divide($a, $b) {
  @return $a / $b;
}

element {
  margin: divide(60, 2) * 1px;
}
```

# SASS: Basic Mixins

- A **mixin** is a reusable piece of code. It is like a variable, but with multiple lines of code.
- Use `@mixin` to name the mixin, and use `@include` to use the mixin.

```scss
@mixin style-link-text {
  text-decoration: none;
  text-transformation: uppercase;
}

.btn {
  @include style-link-text;
}
```

#SASS: Mixins with Arguments

```scss
@mixin style-link-text($col) {
  text-decoration: none;
  text-transformation: uppercase;
  color: $col;
}

.btn {
  @include style-link-text(red);
}
```

# SASS: Extends

- This looks very similar to a mixin, but it works in the opposite direction.

```scss
%btn-placeholder {
  padding: 10px;
  display: inline-block;
  text-align: center;
  border-radiius: 100px;
  width: 100px;
}

/* the following line is added to the above,
  not the other way around (as with a mixin) */
.btn {
  @extend btn-placeholder;
}
```

# NPM: Installing SASS

1. **In your terminal, navigate to the project folder**
2. **Create a `package.json` file by running `npm init`**
   1. This `package.json` file is important, especially when sharing a project with someone else. Instead of sharing the entire `node_modules` folder, you share the `package.json` file. With that, someone can simply run `npm install` (*not* `init`), and it will look at the `package.json` file to download the packages (i.e., the dependencies) that they need to run your project. This is also useful if you yourself want to work on one computer, and then need work on another computer.
3. **Install the SASS compiler by running `npm install node-sass --save-dev`**
   1. The `--save-dev` is so that `package.json` will update and list `node-sass` under 'devDependencies'. A developer dependency is just a tool you use to develop your project. We only need SASS for development purposes. It is not required in the final output itself.
   2. If we were to use just the `--save` tag, it will save it in `package.json` under 'dependencies', not 'devDependencies'. For example, we would install jQuery with `npm install jquery --save`. This is because, unlike SASS, jQuery is required in the final output.
      1. To uninstall jQuery, you would run `npm uninstall jQuery --save`

# Compile SASS Locally

1. **Create a folder named `sass` or `scss`**
2. **Within that folder, create a file named `main.scss`**
3. **To use your `node-sass` package (installed in the last section), you create an `npm script`.**
   1. Within `package.json`, within the `"scripts"` section, add the following (quotations included): `"compile:sass": "node-sass sass/main.scss css/style.css -w"`
   2. The above code is used to specify the following: `"script-name": "package-name input-file output-file -w"`
      1. The "watch" tag, `-w` is what watches your SCSS file for every save, so you don't have to keep manually typing `npm run complile:sass` for every change.
4. **Run your `npm script` in the terminal by running `npm run compile:sass` (or whatever you named the script).**

# NPM Package: Live Server

- This package reloads our complete project as soon as we change any file in the project folder.
- We want to install this package globally (`-g`) on our computer, so we can use it on all future projects and anywhere on our computer. To do this, on your terminal run `npm install live-server -g`
  - If you run into permission error (`ERR!`), simply add the word `sudo` in front of the command.
- Since it is installed globally, we can call it directly from the command line. To run it, go to your project folder, then simply run `live-server` in the command line.

# SCSS: rgba & Hex colors

- In SCSS, you can actually use a hex color or a variable within the `rbga()` parentheses. You cannot do this in regular CSS.

```scss
body {
  background-color: rgba(#873984, 0.8);
}
```

# The :not pseudo-selector

- You can use the `:not` pseudo-selector to select every element of a certain type except for the one you specify. This is often useful for adding a bottom margin to every item except for the last one.

```css
/* Selects every li except for the last one */
li:not(:last-child) {
	margin-bottom: 3rem;
}
```

# Attribute Selectors

```css
[class^="col-"] { ... } // selects classes that BEGIN with "col-"
[class$="col-"] { ... } // selects classes that END with "col-"
[class*="col-"] { ... } // selects classes that CONTAIN "col-" anywhere
```

# SASS: Calc function

- If you insert a variable, you must use `#{$variable-name}`

```scss
.col-1-of-2 {
	width: calc((100% - #{$gutter-horizontal}) / 2);
}
```

# Clearfix

- a clearfix is basically inserting an element after (using `::after`) and then clearing that element

```scss
@mixin clearfix {
  &::after {
    content: '';
    display: table;
    clear: both;
  }
}

/* then, when you want to insert the clearfix, use... */
@include clearfix;
```

# How to give a heading (or any text) a gradient color

```scss
.heading {
  display: inline-block;
  background-image: linear-gradient(to right, $color-primary-light, $color-primary-dark);
  -webkit-background-clip: text;
  color: transparent;
}
```

# Responsive Images

- For the sake of responsiveness, it is usually best to define the width of images in percentages (%), not pixels.

# Responsive Images in HTML - <img> tags

**Density Switching** - image changes based upon *screen resolution*. Serve a larger version of an image for higher resolution screen, and server a smaller version of the same image for a lower resolution screen.

```html
<img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x">
```

- The `1x` and `2x` are density descriptors, for low and high resolution screens, respectively.
- Remember to use `srcset` instead of `src`



**Art Direction** - image changes based upon *screen width*. Use one image on one screen width, and another version (modified) of the image on another screen width

```html
<picture>
	<source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x" media="(max-width: 37.5em)">
	<img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x">
</picture>
```

- The `picture` element allows us to define multiple sources
- The `source` element allows us to write a media query, much like in CSS - `media="(max-width: 37.5em)"`
- If the browser is less than 37.5em, it will use the image in the `source` tag.
- If the browser is greater than 37.5em, it will use the image in the `img` tag.
- Notice that within both the `source` and `img` tags, we are also using Density Switching (see above), in addition to Art Direction



**Resolution Switching** - browser chooses the best image for the current viewport and pixel density situation.

```html
<img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w"
     sizes="(max-width: 900px) 20vw, (max-width: 600px) 30vw, 300px"
     src="img/nat-1-large.jpg">
```



- Width descriptors - `300w` , `1000w` - informs browswer of the width of the images in pixels
- Sizes Attribute - informs the browser of the approximate width of the image at different viewport widths.
- The added `src` attribute at the end is a fallback incase the user is using a browser that doesn't support this method. 

# Responsive Images in CSS

- We simply have to write media queries to load different images in different situations
- The media queries will target device resolution (`min-resolution`), instead of the browser with (as in normal media queries)
- 192 dots per inch is the Apple Retina Screen, and it is a general reference

```css
/* we use min-resolution, and then add a min-width because we don't need
such a large image for smaller screen sizes */
@media (min-resolution: 192dpi) and (min-width: 600px) {
    background-image: linear-gradient(
                      to right bottom,
                      rgba($color-secondary-light, 0.8),
                      rgba($color-secondary-dark, 0.8)),
                      url('../img/hero.jpg');
  }
```



# Browser Support

- Always check caniuse.com before using a modern CSS property in production
- **Graceful Degratation** - using the newest, best features for modern browers, but using alternate options for older browsers.
- Use `@supports` feature query to see if a feature is supported, and if so, add styles within braces

```css
@supports (clip-path: polygon(0 0)) or (-webkit-clip-path: polygon(0 0)) {
	-webkit-clip-path: circle(50% at 50% 50%);
	clip-path: circle(50% at 50% 50%);
	-webkit-shape-outside: circle(50% at 50% 50%);
	shape-outside: circle(50% at 50% 50%);
	border-radius: none;
}
```



# Flexbox Margin Auto

- If you need to make space between flexbox items, but `justify-content` will not suffice, then you can use `margin-right: auto` or `margin-left: auto` to automatically create space between one flex item and the next.
- This is important for situations like headers, where you may want to put two items on the left side and 3 items on the right side. `justify-content: space-between` will not work, so use `margin-right: auto` on the second item to separate the groups.





# currentColor

- setting something to `currentColor` (such as `border-bottom: 1px solid currentColor`) will set it to the same color as the current text color. This is especially helpful for hover effects, where the border-bottom color will automatically change to the color of the text. No need for an extra line to change both the text color and the border-bottom color.



