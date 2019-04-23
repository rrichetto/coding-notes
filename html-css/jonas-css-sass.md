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



