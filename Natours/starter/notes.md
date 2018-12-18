# Notes

## 2.6
### What you will learn
* Best way to perform a basic reset using the universal selector
* How to set project-wide font definitions
* How to clip parts of elements using clip-path

### notes
* use a classname on every selector in html
* always start by using a basic reset.
* jonas just uses the universal selector now, resetting the margin and padding and applying border-box.
* set fonts in body selector, not universal, to preserve inheriting
* use background-image to specify gradients. specify a second with a comma

* background-image: linear-gradient(direction, color, color)
* clip-path: polygon(position 1, position 2, etc)
 * ie polygon(0 0, 100% 0, 100% 70vh, 0, 100%)

## 2.7
### What you will learn
* easiest way to center anything with transform, top, and left

### notes
* better practice to place images in container bc img is inline

## 2.8
### What you will learn
* create css animations using @keyframes and the animation property

### notes
* for browser performance, it's best to only animate two properties: opacity and transform

## 2.9
### What you will learn
* what pseudo-elements and pseudo-classes are
* how and why to use the ::after pseudo-element
* how to create a creative hover animation effect with the transition property

### notes
* always use inline-block if you want to adding padding, width, etc /* why not block?? */
* transform is super important! moving elements, hover effects, etc

## 2.10
### What you will learn
* keep building that button - hover effect animation

### notes
* after pseudoelement

## Section 3: How css works
* getting started with css is easy, but knowing what's going on behind the scenes is more difficult

## 3.12 Three pillars of writing good html and css
* responsive design
* maintainable and scalable code
* web performance

### responsive design
* build a website that works well across all screen sizes.
* a standard today, never build a nonresponsive website!
* FLUID LAYOUTS?
* responsive images
* correct units
* desktop first vs mobile first

### maintainable and scalable code
* more important for you, the developer, than the user
* write code that is clean, easy to understand, supports future growth, and is reusable
* care and think about architecture:
  * how we organize files
  * how we name classes
  * how we structure our html

### web performance
* make apps faster and smaller and size!
* less http requests, less code, compress code, css preprocessor, less images, compress images
* images are usually the far biggest part of a website
* so use images that are only necessary, and compress them!

## 3.13 css behind the scenes - overview
* what happens to our css when we load a webpage?
  * browser loads the html and parses it
  * browser builds DOM from the html
  * as the html is parsed, the css is loaded and parsed (next lecture in detail)
  * two main steps to parsing css:
    * resolve conflicting css declarations through the cascade
    * process final css values - ie converting % to px, etc
  * parsed css is stored in the CSS Object Model (CSSOM)
  * DOM and CSSOM form the render tree, and the page is rendered
  * the page is rendered using the visual formatting model
  * then the website is finally rendered to the screen

## 3.14 how css is parsed: the cascade and specificity
