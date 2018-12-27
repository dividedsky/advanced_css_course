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
* a rule consists of a selector(.my-class) and a declaration block
* each declaration consists of a property and a value (declared value)

### css parsing phase
* first step is to resolve conficting declarations through the cascade
* author declarations are the styles we write
* user declarations are styles changed by user--ie user changing default font size in browser
* browser declarations (user agent) are the default declarations for the browser--ie blue text in links
* when more than once rule applies, the browser looks at the importance(weight), the specificity, and the source order of the declarations

#### importance
* !important, author declarations, user declarations, default browser declarations

#### specificty
* if everything has the same importance, the browser weight specifity
* inline > id's > classes, pseudo-classes, attribute > elements, pseudo-elements
* each selector gets a score: (inline, id, class, elements) ie (0, 1, 2, 2)
* formula: (inline * ) + (id * ) + (classes * ) + elements
* the winning declaration is called the cascaded value

#### source order
* if the specificity of two elements is the same, we go to the source order
* the last declaration in the code will override other declarations and be applied

### final notes
* important has the highest priority, but (so) only use important as a last resource. much better to use correct specificities
* inline styles have higher priority than external stylesheets
* 1 id is more specific than 1000 classes
* 1 class is more specific than 1000 elements
* The universal selector * has no specificity value, so all other selectors have precedence over it
* rely more on _specificity_ than on the _order_ of selectors
* however, when using third-party stylesheets, put your author stylesheet last! this will allow it to override.

## 3.15 Specificity in Practice

* if you need to use !important, that's a bad sign and you should probably refactor
* be careful with selector specificty!

## 3.16 How CSS is parsed, part 2: value processing

* how values are processed in parsing phase
* most common css units and how they are actually calculated
* all units will be convereted to px, and you should know how that happens

### how values are processed
#### declared value -> cascaded value -> specified value -> computed value -> used value -> actual value
* specified value: default value of a css property - more on this later
* computed value: values with relative units are converted to pixels for inheritance
  * also, values like red, orange, etc are computed and converted here
* used value: final calculations based on layout. ex, 66% width calculated based on parent's width
* actual value: values are usually rounded, ie from 184.8px to 185px

### inheritance
* some properties, like the ones related to text, inherit the computed value of their parents

### how units are converted from relative to absolute(px)
* length in %(ie height, margin, padding) the reference is always the parent element's width/length
* ems and rems are font-based. ems use parent element, rems use root font size
* ems for length use the _current element's_ computed font size as a reference
* rem works the same way for font-size and length. ie it uses root for reference.

### why should we size stuff for ems and rems?
* by doing so, we can build more robust responsive layouts because changing font size will change length

### vh and vw
* percentage of viewport height or width
* vh is really useful to build hero sections

### summary
* each property has an initial value, used if nothing else is declared and there's no inheritance
* browsers specify a root font-size for each page (usually 16px)
* % and relative values are always converted to px
* % measured relative to parent's font size if used to specify font size, parent's width is used to specify width
* em are measured relative to their parent's font-size for font-size, or current element's width for width
* rem are _always_ measured relative to the root font-size
* vh and vw are simply % measurements of the viewport's height and width

## How CSS Is Parsed, Part 3: Inheritance
* every css property must have a value, even if we nor the broswer specify it
* first question css engine asks is, 'is there a cascaded value?'
* if no, it asks if the property is inherited
* some properties are inhereted, and some are not
* mdn specs show whether props are inherited
* if it is inherited, property becomes _computed_ value of its parent element
* if it is not inherited, specified value will become initial value (also in mdn specs)
* properties related to text are inherited: font-family, font-size, color
* other properties, such as margin, padding, etc are not inherited
* inheritance only works if no one declares a value for that property
* we can use the inherit keyword to force inheritance on a certain property
* we can use the initial keyword to reset a property to its initial value
