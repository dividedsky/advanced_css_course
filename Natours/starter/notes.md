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

## 3.17 How CSS Is Parsed, Part 3: Inheritance
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

## 3.18 Converting px to rem: an effective workflow

### what you will learn
* how and why to use rem units
* a great workflow for converting px to rem

### notes
* we want an easy way to change all the measurements on our page to one simple setting
* instead of writing hundreds of lines of media queries, we can just change the global font size
* rem unit is always in relation to root font size
* setting root font size allows us to change all our px font sizes to rem
* change the root font size to 10px...is this better than 62.5% -- no!!
* keep in mind that rems are not supported below IE9. but i don't really care :-/
* move box-sizing from universal selector to body, set box-sizing in universal selector to inherit

## 3.19 how css renders a website: the visual formatting model
* css visual formatting model is an algorithm that calculates boxes and determines the layout of these boxes for each element in the render tree in order to determine the final layout of the page
* one of the fundamental concepts of css
* takes into account dimensions of the boxes (the box model), box type (inline, block, inline-block), positioning scheme(floats and positioning), staching contexts, other elements in the render tree, viewport size, img dimensions, etc
* FILL AREA: the area that gets filled with the background color or background image - includes the padding and the border, but not the margin
* height and width without border-box: borders + padding + width/height
with border-box: width/height

### box types: inline, block-level, inline-block
#### block-level
* display is usually set to block, but also could be flex, list-item, or table
* p and div have their display set to block by default
* block-level box will always occupy as much space as possible--usually 100% of parent's width
* displayed vertically, one after another

#### inline
* content is distributed in lines
* occupies only the content's space
* no line breaks
* no height and width
* padding and margins only horizontal (left and right)

#### inline-block
* a mix of block and inline
* technically, they are inline elements that use the block model on the inside
* occupies only the content's space
* no line breaks
* box-model applies just as in regular block-level boxes

### positioning schemes: normal flow, floats, absolute positioning
#### normal flow
* default positioning scheme
* not floated and not absolutely positioned
* relative positioning still uses the normal flow
* elements are laid out on page according to their source order

#### floats
* element is removed from the normal flow and shifted to the left or right
* texts and inline elements will wrap around the floated element
* container will not adjust its height to the element, which can be problematic and is usually fixed with clear fixes

#### absolute positioning (and fixed)
* element is removed from the normal flow
* _no impact on surrounding content or elements_
* top, bottom, left, and right are used to offset the element from its relatively-positioned container

### stacking contexts
* determines in which order elements are rendered on the page
* z-index is the most widely-used stacking context property
* layers on the bottom of the stack are painted first, layers on the top are painted last, overlapping items below them
* highest z-index appears on top, lowest z-index on the bottom
* stacking context also affected by opacity different from 1, a transform, a filter, or other properties

## 3.20 css architecture, components, and BEM
* We want css code that is clean, modular, reusable, and ready for growth
* need to think about architecture right from the beginning of the project
* best strategy is think -> build -> architect mindset
* think about the layout before we actually wriet the code
* then build it in html and css with a consistent structure for naming classes
* create a logical css architecture by using multiple files and folders

### think
* component-driven design: modular building blocks that make up interfaces
* our interface is a collection of components held together by the overall layout of the page
* components should be reusable across a project, and between different projects
* build a library of your components!!
* components should be independent so they can be used anywhere on the page
  * this means that components should not be dependent on their parent elements!
* this is similar to atomic design:
  * smallest elements on a page are atoms, which form molecules, which form organisms

### build
* consistent approach to naming your classes!
* many approaches--object-oriented css, etc--but BEM is what Jonas prefers

#### BEM: Block Element Modifier
* block is a standalone component that is meaningful on its own 
* an element is a part of a block that has no meaning on its own: block__element
* modifier is a flag we can put on the block or element to make it different: block__element--modifier

### architect
* logical folder and file structure for folder to live in
* different methods, but Jonas uses the 7-1 pattern
* 7 different folders for partial Sass files, and one main Sass file to import others into a compiled Sass sheet
* 7 folders: base, components, layout, pages, themes, abstracts, vendors
  * base: basic product definitions
  * components: 1 file for each component
  * layout: overall layour
  * pages: styles for specific pages
  * themes: different visual themes
  * abstracts: code that doesn't output css, such as variables and mixins
  * vendors: third-party css

## 3.21: Putting BEM into practice
* convert html/css into BEM naming

## 4.22 Sass intro

## 4.23 What is Sass?
* Sass is a CSS preprocessor, an extension of css that adds power and elegance
* Sass source code is compiled into css code

### Sass features
* _variables_ for reusable values such as colors, font-sizes, etc
* _nesting_ to nest selectors inside one another
* _operators_ for math operations inside of css
* _partials and imports_ to write css in different files and import them all into one file
* _mixins_ to write reusable pieces of css
* _functions,_ similar to mixins, with the difference being they produce a value that can be used
* _extends_ to make selectors inherit declaratinos that are common to all of them
* _control directives_ for writing complex code using conditionals and loops (not covered in this course)

### sass vs scss: clearing up the confusion
* SCSS is Sassy CSS
* Sass syntax is indentation sensitive, doesn't use semicolons or brackets
* scss syntax preserves the original css syntax

## 4.24 First steps with sass: variable and nesting

* variables with $
* comments with //
* nesting and & operator
* floats and clearfix
* color functions! ie &:hover {
    background-color: darken($color-secondary, 15%);
}

## 4.25 First steps with sass: mixins, extends, and functions

### Mixins
* a reusable piece of code written into a mixin. when the mixin is used, code is tranferred
* clearfix example: 
```
@mixin clearfix {
    &::after {
        content: '';
        clear: both;
        display: table;
    }
}

nav{
@include clearfix;
}
```

* common props example (DRY)
    ```
    @mixin style-link-text($color) {
        text-decoration: none;
        text-transform: none;
        color: $color;
    }

    a:link {
    @include style-link-text($color-text-dark);
    }
    ```

### functions
* darken is an example of a function, but we can write our own, as well
* takes arguments, just as a mixin does
* Jonas does not find them so useful as mixins

* example:
```
@function divide($a, $b) {
    @return $a / $b;
}

margin: divide(60, 2) * 1px; //30px...use * 1px to convert to px
```

### extends
* write a placeholder, put styles in, and have other selectors extend the placeholder
* example on buttons with duplicate styles:
```
%btn-placeholder {
    padding: 10px;
    display: inline-block;
    text-align: center;
    border-radius: 100px;
    width: $width-button;
    @include style-link-text($color-text-light);
}

.btn-main {
    &:link {
        @extend %btn-placeholder;
    }
}
```

* why use extends instead of mixin?
* in a mixin, the code is copied. with an extends, the selector is copied!
* you should only use extends if the rules you are extending are inheritenly related
* Jonas is not such a big fan of extends and prefers to use mixins. However, sometimes extends is the correct tool to use.

## 4.26 a brief intro to the command line

## 4.27 npm packages: installing sass locally
