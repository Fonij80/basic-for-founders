# Cascading Style Sheets (CSS)

## Definitions

- Descendant: an element within the child hierarchy

- Viewport: the page area which is visible in your browser

### Syntax Rules

```CSS
.class_selector {
    property: value value ...;
}

/* Property conflicts */
.class_selector {
    same_property: value1;
    same_property: value2;
    /* value2 will be applied */
}
```

### At-rules

- An at-rule is a special CSS rule that acts as a directive controlling the behavior of CSS.
  - @charset: Defines the character encoding used in the CSS file.

  - @import: Imports, or includes, the contents of another style sheet.

  - @media: Defines a media query.

  - @keyframes: Defines a set of keyframes for a CSS animation.

### 3 Ways Of Using CSS

```HTML
<!-- Inline (top priority to be applied) -->
<div style="background-color: red;">
  Hello world!
</div>

<!-- Internal, in <head> -->
<!DOCTYPE html>
<html>
  <head>
    <style>
      div {
        background-color: red;
      }
    </style>
  </head>
  <body>
    <div>Hello world!</div>
  </body>
</html>

<!-- External, use .css file -->
<!DOCTYPE html>
<html>
  <head>
    <link rel="stylesheet" href="/path/to/file.css">
</head>
  <body>
    <div>Hello world!</div>
  </body>
</html>
```

### CSS Preprocessors

- provide extended syntax for writing CSS rules and convert your CSS into plain CSS for the browser such as Sass, LESS, Stylus
  1. Nested rules: not supported in css but can be used by preprocessor

  ```CSS
  <!-- nested selctors in Sass -->
  .header {
    background-color: red;
    h1 {
      font-size: 24px;
    }
  }

  <!-- the equivalent CSS -->
  .header {
    background-color: red;
  }
  .header h1 {
    font-size: 24px;
  }
  ```

  2. Variables: not supported in older browsers

  ```CSS
  <!-- Sass variable -->
  $header-color: red;
  .header {
    background-color: $header-color;
  }
  ```

  3. Mixins: allows you to write a set of CSS properties and values, then apply that entire set of properties to another CSS rule without having to repeat all the code
  - useful for cutting down on duplicated code. They can even take arguments to customize the resulting CSS.

  ```CSS
  <!-- Sass felxbox mixin (used in older browser) -->
  @mixin flexbox {
    display: -webkit-flex;
    display: -ms-flexbox;
    display: flex;
  }

  <!-- applying the mixin -->
  .header {
    @include flexbox;
  }
  ```

### How CSS works in the browser?

- DOM: data structure in the browser, a tree of objects that represent the elements in the document and their structure and hierarchy, created by reading the HTML markup, tokenizing it, parsing it, and finally creating the object hierarchy that makes up the DOM.

- CSSOM: a tree structure that shows the hierarchy of styles in the document, browser parses CSS and creates CSSOM

- Render Tree: combination of DOM & CSSOM, contains all the info browser needs to render a page

- after creating render tree, browser begin laying out the elements on the page and then paint the page by applying styles

## CSS Selectors

1. Universal: matches all elements

```CSS
/* removing all margins */
* {
  margin: 0;
}
```

2. Element: target an element by its tag name

```CSS
/* applying margin to all p */
p {
  margin: 25px;
}
```

3. ID: use the value of _id_ attribute, element's id must be unique but if there are multiple elements with the same id, most browsers will match the rule with all alements having that id

```CSS
/* applying padding to element having header id */
#header {
  padding: 25px;
}
```

4. Class: use the value of _class_ attribute

- class can be used to mark all elements of a related type, a single element can have any number of classes

```CSS
/* applying color to all elements having nav-link class */
.nav-link {
    color: blue;
}
```

5. Attribute: an element can be selected by its attribute value or the presence of an attribute

- [name]: selects all elements that have the given attribute, regardless of its value

- [name="value"]: Selects all elements that have the given attribute, whose value is the string value.

- [name~="value"]: Selects all elements that have the given attribute, whose value contains the string value separated by whitespace.

<div title="Hello World">Hello World</div>
<div title="HelloWorld">HelloWorld</div>

- If we wrote a CSS rule with the selector [title~="World"], the first element would match but not the second. This is because in the second element, the word “World” in the title attribute is not surrounded by whitespace.

- [name*="value"]: Selects all elements that have the given attribute, whose value contains the substring value. If we wrote another CSS rule, this time with the selector [title*="World"], it would match both of the preceding elements.

- [name^="value"]: Selects all elements that have the given attribute, whose value begins with value.

- [name$="value"]: Selects all elements that have the given attribute, whose value ends with value.

6. Compound: all selectors (except \*) can be used alone or in conjucation with other selectors

```CSS
/* Matches all div elements with a class of my-class. */
div.my-class

/* Matches all span elements with a class of both class-one and class-two. */
span.class-one.class-two

/* Matches all a elements with a class of nav-link that have an href attribute that
contains the string example.com. */
a.nav-link[href*="example.com"]
```

7. Multiple independent selectors

```CSS
/* Matches all elements with a class of class-one as well as all elements with a class of class-two. */
.class-one, .class-two
```

## Selector Combinators

- used to select more specific elements

1. Descendant: matches an element that is a descendant of the element on the left-hand side

```CSS
/* Matches all div elements that are direct or indirect children of an element with a class of header. */
.header div
```

2. Child: matches an element that is a direct child of the element on the left-­ hand side

```CSS
/* Matches all div elements that are direct children of an element with a class of header. */
.header > div
```

3. General sibling: matches an element that is a sibling, but not necessarily an immediate sibling, of the element on the left-hand side

```HTML
<div>
  <div class="header"></div>
  <div class="body"></div>
  <div class="footer"></div>
</div>

<!-- The selector .header ~ div would match two div elements: the one with class body and the one with class footer. Note that it does not match the div with class header. -->
.header ~ div
```

4. Adjacent sibling: only matches elements that are an immediate sibling

```CSS
/* match the body element, because it is the adjacent sibling of the heading element */
.header + div

/* multiple combinator */
/* this selector will match a button element that is an immediate sibling of a div element, which in turn is an immediate child of a div with the class header */
div.header > div + button
```

## Pseudo-classes

- allows you to select elements based on UI state or its position in the document

1. UI state:
   - :active: currently being activate, pressed but bot yet released for button and links

   - :checked: a checked radio button, checkbox, or option inside a select

   - :focus: currently has the focus, for buttons, links and text fields

   - :hover: mouse cursor is currently hovering over, usually for buttons and links

   - :valid, :invalid: used with form elements usind HTML5 validation

   - :visited: a link whose URL has already been visited by the user

2. Document structure
   - :first-child, :last-child: first/last child of its parent

   - :nth-child(n): matches an element that is the nth child of its parent

   ```HTML
   <ul class="my-list">
     <li>Item one</li>
     <li>Item two</li>
   </ul>

   <!-- matches Item one -->
   .my-list > li:nth-child(1)

   <!-- matches Item two -->
   .my-list > li:nth-child(2)

   <!-- matches every other list item -->
   .my-list > li:nth-child(2n)

   <!-- matches every four items -->
   .my-list > li:nth-child(4n)

   <!-- matches all odd-numbered children -->
   .my-list > li:nth-child(odd)

   <!-- matches all even-numbered children -->
   .my-list > li:nth-child(even)
   ```

   - :nth-of-type(n): Similar to :nth-child, except that it only considers children of the same type

   ```CSS
   <!-- matches any div element that is the second div element among any group of children -->
   div:nth-of-type(2)
   ```

   - :root: matches root element of the document (<html>), used for declaring global vars

## Negating a selector

- :not() accepts a selector as an arg and will match any element for which the selector does not match

```CSS
/* matches any div that does not have the fancy class */
div:not(.fancy)
```

## Pseudo-elements

- allows you select only part of a matched element, some pseudo-elements only apply to block-level elements
  - ::first-line: matches the first line of a block element

  - ::first-letter: applies the styles only to the first letter of the first line of an element

  - ::before, ::after: create a new element as either the first child or the last child of the matched element, respectively, used to decorate or add effects to an element, you must always provide _content_ property or the element won't be shown

  ```HTML
  <a class="external-link"
     href="https://google.com">
    Google
  </a>

  <!-- external link indicator, shows the link like: Google (external) -->
  <!-- add the content (external) and made it green -->
  .external-link::after {
    content: ' (external)';
    color: green;
  }
  ```

## Specificity

- When there is a conflict of CSS properties across multiple rules, the rule with the most specific selector will be chosen.

- specifity rankings:
  1. Inline styles in an element’s style attribute

  2. ID selectors

  3. Class selectors, attribute selectors, and pseudo-classes

  4. Element selectors and pseudo-elements

\*\* Neither the universal selector nor combinators factor into specificity.

- if multiple conflicting rules are calculated to have the same specificity, the rule that appears last will win. (specifity calculator)

```HTML
<style>
  .profile {
    background-color: green;
  }
  div {
    background-color: red;
    color: white;
  }
</style>
<div class="profile">My Profile</div>
<!-- background will be green -->
```

- _!important_: this keyword cause the property to always win in a conflict, but it is a bad practice and make your style sheet less maintainable

## Box Model

- element in CSS -> like a rectangular box: margin, border, padding, content.

- By default, most elements have no padding, border, or margin.

- width & height depends on _box-sizing_ which supports _content-box_ & _border-box_

- content-box:
  - deafult
  - width & height properties are treated as the size of content-area only
  - actual width & height = width and height (the content box) + the padding on each side + the border width on each side

- border-box:
  - width & height properties are treated ad the size of content box + padding and border with.

```CSS
display: inline, block, inline-block;
```

### Block element

- always appears on its own line

- takes up the full width of its containing element, unless an explicit width is set with the _width_ property

- its height is, by default, just enough to fit the height of its content

### Inline element

- rendered inside the normal flow of text

- takes up enough widht and height as necessary to contain the content

- no effect in setting _width_ and _height_

- left and right padding/margin increase the width

- but top and bottom padding/margin don't work as expected

### Inline-block element

- flows with the text like an inline element, but the width and height properties are respected, as are the vertical padding and margin.

## Units

### px

- If CSS used device pixels, then a 1-pixel border would barely be visible to the user.

- It is generally not recommended to use px units in CSS. The main reason is that these pixel-based dimensions don’t always scale well when a user adjusts the browser zoom level. This can be an accessibility issue.

- use it for _font-size_ (its default is 16px) and media query

### em

- realtive to the font size of the element

```CSS
.header {
    font-size: 24px;
    padding: 0.5em; /* ~= 12px */
}
```

### rem (root em)

- relative to page's base font size

- If the browser is zoomed, everything resizes nicely because it’s all proportional to the base font size.

### vw and vh (viewport width and height)

- 1vw = 1% of viewport width

- 1vh = 1% of viewport height

- used in responsive design

- vmin: min(vh, vw)

- vmax: max(vh, vw)

### %

- relative to the size of another value, used in responsive design

- % for font-size is relative to parent element's font size

- % for padding is percentage of element's width

### other units

- used for print style sheet not in screem style sheet

- cm, mm, in (inches), pt (points)

### calc

- CSS built-in function, calculate the difference between different units (calc(1.5rem - 10px))

## Overflow

- when an explicit height is set and the content does not fit inside the element's dimensions

- the content inside a block element will wrap to a new line when it doesn’t fit horizontally

- use _overflow_ property (overflow-x and overflow-y independantly), default value is visible

```CSS
/* cause horizontal overflow */
white-space: nowrap;

/* overflowing content is simply not
displayed */
overflow: hidden;

/* user can scroll to see the overflowing content, scrollbar always provided even when not overflow */
overflow: scroll;

/* scrollbar only provided if the content actually overflows */
overflow: auto;
```

## CSS variables (custom properties)

- Variables cascade down to descendant elements.

```CSS
/* variable definition */
--brand-color: #ffffff;

/* variable referencing */
background-color: var(--brand-color);

/* var func takes a fallback value as the second arg */
background-color: var(--brand-color, #000000);

/* global var */
:root {
    --text-color: red;
}

/* referencing variables inside other variables */
:root {
    --primary-border-color: red;
    --primary-border-style: solid;
    --primary-border-width: 3px;
    --primary-border:
      var(--primary-border-width)
      var(--primary-border-style)
      var(--primary-border-color);
}
```

## Global Property Values

- initial: Uses the initial value set by the browser’s built-in style sheet.

- inherit: Takes the value used by the element’s parent.

- unset: If the property naturally inherits from its parent, such as font-size, it is set to the inherited value. Otherwise, it is set to the initial value from the browser’s style sheet.

## Shorthand properties

- 1 value: all sides

- 2 values: top/bottom, right/left

- 3 values: top, right/left, bottom

- 4 values: top, right, bottom, left (clockwise)

- Each shorthand property has four equivalent properties for each side of the element.

- For example, for the padding shorthand element, there are also padding-top, padding-­bottom, padding-left, and padding-right properties.

## Border properties

- border-color

- border-width

- border-style: none, solid, dotted, dashed, double, groove, ridge, inset, outset

- border-collapse:
  - only applies to _table_
  - default value is _separate_ -> table borders are not combined
  - value: collapse -> Any cell borders adjacent to another border have been collapsed into a single border.

- border-radius:
  - default element radius: 90 degree corners

```CSS
/* border shorthand */
border: 5px solid red;

/* circular border radius */
border-radius: 10px;

/* Using an elliptical border-radius */
border-radius: 20px / 10px;

/* differnt border radius */
border-bottom-right-radius: 10px 20px;
border-bottom-left-radius: 5px;
border-top-left-radius: 20px 10px;
border-top-right-radius: 50%;
```

## Box Shadow

- color
- X offset: neccessary
- Y offset: neccessary
- Blur radius: How far out the shadow is blurred, default zero
- Spread radius: How far the shadow extends beyond the element’s dimensions, default zero

```CSS
/* X offset, Y offset, blur radius, spread radius (outer) */
box-shadow: 5px 5px 10px 5px black;

/* box shadow inside the element (inner) */
box-shadow: 0 0 25px black inset;

/* multiple shadows */
box-shadow: 0 0 10px 0 black, 0 0 25px red inset;
```

## Opacity

- default: trasparent background for elements
- by adding color or image, element became opaque
- borders and text -> opaque
- opacity can be set for all elements, from 0 to 1

## Hiding elements

- display: none -> as if the elements doesn't exist, other elements fill its empty space
- visibility: hidden -> the flow of document (layout) is not affected, empty space will replace the element
- opacity: 0 -> same as visibility

## Interesting To Know

- CSS was published in 1996.

- Styles **cascade** from less specific to more specefic selectors.

- Before CSS, styling was specified using HTML attributes -> tight coupling between semantics and presentation

- Table as a layout -> hard for screen reader to navigate

## Backgrounds

- used for any element

- url func arg: absolute/relative URL

- element larger than bg-image -> image will be repeated to fill the element by default

- By default, an element’s background goes behind its border, padding, and content -> set background-clip

- Background shorthand exceptions:
  - The background-size must come directly after background-­position, separated by a slash.

  - The background-color must come last.

```CSS
/* different value options separated by , */
/* solid bg color */
background-color: #FF0000;

/* one/more bg image(s), stacked on top of each other */
background-image: url('tiles.jpg');

background-repeat: no-repeat, repeat-y, repeat-x;

/* first value: position on X-axis, second value: position on Y-axis */
background-position: top, bottom, left, right, center, 10px;

background-size: cover, contain, 10px 5px;

/* content-box: bg only behind content not padding and border */
background-clip: border-box(default), padding-box, content-box;

/* shorthand */
background: url('mountains.jpg') center / cover;
```

## Gradients

- modern browsers support gradients but before that you must set the bg-image which has gradient

### Linear

- default: top to bottom with evenly distributed stops

```CSS
/* with 3 stops */
background-image: linear-gradient(red, blue, green);

/* using trasnparency */
background-image: linear-gradient(
      transparent,
      blue,
      transparent
    );

/* Specifying the gradient direction with customizing stops */
background-image: linear-gradient(
      to right,
      red 0%,
      green 25%,
      green 75%,
      blue 100%
    );

/* Specifying an angle for the gradient */
background-image: linear-gradient(
      45deg,
      red,
      blue
    );
```

### Radial

- A radial gradient starts at a central point and radiates outward.

```CSS
/* A radial gradient */
background-image: radial-gradient(red, blue);

/* Specifying a circle for the radial gradient shape */
background-image: radial-gradient(
      circle,
      red,
      blue
    );

/* Specifying the position of the gradient shape (<shape> at <position>)*/
/* circle's center at 25% of X axis */
background-image: radial-gradient(
      circle at 25%,
      red,
      blue
    );

background-image: radial-gradient(
      circle at top left,
      red,
      blue
    );

/* A radial gradient with multiple color stops    */
background-image: radial-gradient(
      red,
      blue,
      green 75%
    );

/* multiple gradients */
background-image: radial-gradient(
      ellipse at 25%,
      red,transparent
    ), radial-gradient(
      ellipse at 75%,
      blue,
      transparent
    );

/* Applying a lighting effect with a gradient to bg-image */
background-image:
      radial-gradient(
        ellipse at top left,
        white 25%,
        transparent
      ),
      url('mountains.jpg');
```

The size of the gradient can be further influenced by providing modifiers to the shape that define where the gradient should end. The options that can be set are:

- closest-side: The gradient ends at the side closest to the center of the gradient. For a wide rectangle, this would be the top or bottom.

- farthest-side: The gradient ends at the side farthest from the center of the gradient. For a wide rectangle, this would be the left or right.

- closest-corner: The gradient ends at the closest corner to its center.

- farthest-corner: The gradient ends at the farthest corner from its center. This is the default.

## Text Styling

- web-safe fonts (available on most user's systems):
  - Arial, Trebuchet MS, Verdana (sans-serif)
  - Courier New (monospace)
  - Georgia, Times New Roman (serif)

- font-family: The browser will try each font, starting with the first, until a match is found, last font is typically a generic one, where the browser will use a fallback font that approximates the desired appearance

- font-size:
  - An element inherits its parent's font size by default.
  - font-size can also be specified as a percentage of its parent's size
  - base doc font size: 16px
  - predefined value: from xx-small to xxx-large
  - em: relative to parent element
  - rem: relative to root element

- white-space:
  - normal: The default behavior. Whitespace is collapsed, and text is automatically wrapped as needed.

  - nowrap: Same as normal, except that lines of text do not wrap.

  - pre: respect the whitespaces with no wrap

  - pre-wrap: Same as pre, except that lines of text are also wrapped.

  - pre-line: Same as pre-wrap, except that consecutive whitespace characters are collapsed. Line breaks are still preserved.

  - break-spaces: Same as pre-wrap, except that line wrapping behavior is slightly different. Not supported in Internet Explorer.

```CSS
/* use ' for space-containing font name*/
font-family:
    Georgia,
    'Times New Roman',
    serif;

font-size: 1.5em;

color: red;

/* how bold the text appears */
/* normal = 400, bold = 700, lighter & bolder in relative to parent */
font-weight: normal, bold, 100, 900, lighter, bolder;

font-style: normal, italic, oblique;

text-decoration: underline, line-through, none;
/* text-decoration styles: solid, double, dotted, dashed, wavy */
text-decoration: underline solid blue;

text-transform: uppercase, lowercase, capitalize, none;

/* adjust space between each letter */
letter-spacing: 5px;

/* All lowercase letters are transformed into smaller-sized capital letters */
font-variant: small-caps;

/* indent of first line */
text-indent: 50px;

/* how whitespace is handled inside an
element that contains text */
white-space: normal (default), pre;

/* Truncating text (no overflowing or wrapping) */
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;

/* add spacing between lines */
line-height: 5px;

text-align: center, left, right, justify;

/* X offset, Y offset, blur radius, color */
text-shadow: 2px 2px 0px red;
```

- Horizontal alignment
  - text-align: only has an effect on block elements with a width greater than that of their content, It sets the horizontal alignment of any inline element inside the containing element on which text-align is set.

- Vertical alignment
  - If a block element's height is taller than its content, by default the text will be aligned to the top of the container.

  - setting _vertical-align_ has no effect, set the _line-­height_ to the same as the container _height_

  - _vertical-align_ controls how inline elements are aligned vertically with each other

- We gave one element a color of red and the other a color of blue. This set the currentColor value of each element. Then, we also had a rule that selected both div elements and used the currentColor as the border color. The red div gets a red border, and the blue div gets a blue border.

```HTML
<!-- use of color and currentColor -->
<style>
  div {
    border: 3px solid currentColor;
  }
  .one {
    color: red;
  }
  .two {
    color: blue;
  }
</style>
<div class="one">One</div>
<div class="two">Two</div>
```

## Using web fonts

- browser can download the font file

- supported formats:
  - Web Open Font Format version 1 or 2 (WOFF/WOFF2)
  - Embedded Open Type (EOT)
  - TrueType Font (TTF)
  - Scalable Vector Graphics (SVG)

- @font-face: declares a new font, use the font by _font-family_

- use Web Font Loader tool to decrease the effect of the flash of unstyled/invisible text

```CSS
@font-face {
  font-family: 'SomeWebFont';
  src:
    url('/some-font.woff2') format('woff2'),
    url('/some-font.woff') format('woff');
}
body {
  font-family: SomeWebFont, Arial, sans-serif;
}

/* Defining two weights of a web font */
@font-face {
  font-family: 'SomeWebFont';
  src: url('/some-font.woff2') format('woff2');
  font-weight: 400;
}

@font-face {
  font-family: 'SomeWebFont';
  src: url('/some-font-bold.woff2') format('woff2');
  font-weight: 700;
}
```

## Layout and Positioning

### Padding

- elm padding not inherited by its children, specified with any size unit/percentage

### Margin

- specified with any size unit/percentage or keyword _auto_

- margin: auto: When the horizontal margin = auto in a block/inline-block element, the element is centered horizontally within its containing element but **not true** for vertical margin

- Margin Collapse: When two elements with a vertical margin meet vertically, the two margins are collapsed into a single margin, the collapsed margin will take the size of the larger margin

**Margin collapse applies to vertical margins only.**

- Another situation where the vertical margins collapse is when there is no border, padding, or other content between a parent and its child.

### Positioning

- If an element’s position property is set to any value other than static, it is considered a _positioned element_.

- position: static: default value, positioned in the normal flow of the document, When position is set to static, the top, right, bottom, and left properties have no effect.

- position: relative: positioned relative to where it would normally appear in the flow of the document, If position is set to relative, but top, right, bottom, or left are not specified, it essentially has the same effect as if position were set to static but has effect on the child element
  - Generally, if both top and bottom are specified, the top value is used, and the bottom value is ignored. Similarly, if both left and right are specified, left wins if the text direction is left to right and right wins if the text direction is right to left.

- position: absolute: an absolutely positioned element is removed from the document flow and “floats” above it. The layout of other elements will be adjusted as if the absolutely positioned element is not there.
  - While a relatively positioned element’s offsets are relative to the element’s original position in the document, an absolute positioned element’s offsets are relative to the closest ancestor positioned element (not necessarily the element’s direct parent), if no ancestor positioned -> positioned relative to the document

- position: fixed: removes the element from the document’s flow and all offsets are relative to the viewport (in contrast of absolute), in page scrolling -> remain in the same position
  - A block element with a position of static or relative will, by default, take up the full width of its container. However, if an element is given a position of absolute or fixed, this will no longer be the case. It will only be as wide as it needs to be to fit its content. This can usually be solved by adding a width: 100% to the element if the full width behavior is still desired.

- position: sticky: a combination of relative and fixed. The element acts as a relatively positioned element, scrolling with the document. When the element reaches a specified point, it turns into a fixed element. This point is specified via a top, right, bottom, or left value.

- Statically positioned elements flow normally.

- Relatively positioned elements are positioned relative to their normal position in the document.

- Absolutely positioned elements are positioned relative to their nearest positioned ancestor.

- Fixed-positioned elements remain fixed to the viewport.

- Sticky-positioned elements are a hybrid between relative and fixed position.

## Z-index and Stacking Contexts

- position of fixed, absolute, sticky -> can obscure other elements

- z-index determines the stacking order of elements along the z-axis, relative measure, can take any numberic value

### Stacking contexts

- As it turns out, z-index doesn’t control an element’s z-axis ordering globally within the entire document. It only controls the z-index relative to other elements within a given stacking context.
  - Initial context: html element
  - other elements that can create a new stacking context:
    - Any element that has a position other than static and a z-index other than auto
    - Any element with an opacity less than 1
    - Any element that is a child of a flex or grid container and a z-index other than auto

- If no z-index is given, there are certain stacking rules that are applied inside a stacking context:
  - The background and borders of the element that creates the stacking context
  - Descendant elements of the element that creates the stacking context that are not positioned
  - Descendant elements of the element that creates the stacking context that are positioned

## Floats

- use the float property to make an element “float” to the left or the right and text and other inline elements will flow around it

- When the float property is applied to an element, it is removed from the flow of the document. It then “floats” to the left or right, stopping when it reaches the edge of the containing element, or another floated element.

- float: right, left, inline-start, inline-end

### Clearing floats

- The clear property can be used on an element to indicate that it can’t be alongside a floated element in a given direction. The clear property can be none (the default), left, right, both, inline-start, or inline-end. If an element is cleared in a given direction, and there is a floated element there, the element will be moved so that it is below the floated element.

## Transforms (for creating effect on elements)

### Perspective

- activate 3D space, defines how “far away” the object is from the user, as if the screen had depth

### Rotation

- rotate element around a given axis

- when an element is rotated, the axes move with the element as well.

- angle rotation units:
  - deg(Degrees): full circle = 360deg
  - grad(Gradians): full circle = 400grad
  - rad(Radians): full circle = 2π radians or 6.28rad
  - turn: full circle = 1 turn

- Axis:
  - X: left to right
  - Y: top to bottom
  - Z: surface toward you

- Origin: element is rotated around the origin point, center of element by default, set different origin by _transform-origin_

- rotate/rotateZ function: same effect, rotate element around Z-axis

- rotateX around X-axis

- rotateY around Y-axis

- rotate3d around an arbitrary axis in 3D space

```CSS
transform: perspective(200px) rotateY(45deg);

transform: perspective(200px) rotate3d(1, 1, 0, 45deg);

/* translated 2rem to the left and 2rem down, (X-axis, Y-axis) */
transform: translate(2rem, 2rem);

/* == translate(1rem, 0) */
transform: translateX(1rem);

/* == translate(0, 1rem) */
transform: translateY(1rem);

transform: perspective(200px) translateZ(2rem);

/* like rotate3d, specify a vector in 3D space and then translate the element */
transform: perspective(200px) translate3d(1rem, 2rem, 3rem);

transform: scale(2, 5);

transform: scaleX(2);

transform: scaleY(5);

transform: scaleY3d(2, 3, 5);

transform: skew(45deg, 20deg);

transform: skewX(45deg);

transform: skewY(20deg);

/* allow child elements to exist in 3D space */
transform-style: preserve-3d;
```

### Translate

- Translating an element means moving it from its original position in 2D space.

- translateZ: It has the effect of moving an element closer to or farther away from the user’s perspective. It only has a visible effect when used in combination with the perspective function.

### Scaling

- A scaling transform function alters the size of the element, scaling its contents as it grows or shrinks.

- _scale(1, 2)_ -> no scaling

- _scale(2, 3)_ -> scale the element to two times as large in the horizontal direction and three times as large in the vertical direction

- By default, the scaling functions perform the transform starting at the center at the element. This can be changed by giving a value for the transform-origin property.

- scaleZ effect is best seen when used in combination with perspective and another transform like rotateX

### Skewing

- distort an element by a given angle in X and Y directions

## Transitions

- a way of animating an element from one state to another

- time units: s or ms

- default transition timing function (**ease**): start out slow, speed up in the middle, then slow down again at the end

- timing function === easing function

- easing function are given as Cubic Bezier curves which is created by specifying four points on a graph -> start state of transition: (0, 0), end state: (1, 1)

- for defining your own easing fucntion just give X and Y of the two middle point as an args to cubic-bezier

- The animation progress (the Y-axis) can also bend above 1 or below 0 to create a “bouncing” effect for some properties like cubic-­bezier(0.680, -0.550, 0.265, 1.550)

- Easing functions can also be specified as step functions. A step function divides the transition into equally sized steps in a given direction. Instead of a smooth transition like with a Bezier curve, they jump from step to step, skipping the intermediate states.

- These are specified as steps(step-count, direction). step-count is a number indicating the number of these steps, and direction is one of the following values:
  - jump-start, start: The change in state happens at the beginning of each step, beginning with the start of the transition. Because the first “jump” happens immediately, the initial state of the transition is effectively lost.

  - jump-end, end: The change in state happens at the end of each step,
    ending with the end of the transition. With this value, the end state of
    the transition is lost.

  - jump-none: With this value, the start and end state of the transition are both preserved. The first step is the initial state, and the last step is the end state.

  - jump-both: With this value, the start and end state of the transition are both lost.

```CSS
/* shorthand transition args: property, duration , delay */
transition: 300ms;

/* Transition the color over 500 milliseconds. */
/* Transform the scale over 500 milliseconds, with a 500-millisecond delay. */
transition: background-color 500ms transform 500ms 500ms;

transition-property: background-color transform;
transition-duration: 500ms, 500ms;
transition-delay: 0ms, 500ms;

/* define your own easing function */
transition-timing-function:
  cubic-bezier(.17, .67, .9, .6);

/* built-in easing function */
/* cubic-bezier(0.0, 0.0, 1.0, 1.0) */
linear

/* cubic-bezier(0.25, 0.1, 0.25, 1.0) */
ease

/* cubic-bezier(0.42, 0.0, 1.0, 1.0) */
ease-in

/* cubic-bezier(0.0, 0.0, 0.58, 1.0) */
ease-out

/* cubic-bezier(0.42, 0.0, 0.58, 1.0) */
ease-in-out
```

## Animations

- Where CSS transitions provide an animated transition from a start state to an end state, animations provide animated transitions between any arbitrary number of states.

### Animation Properties

- animation-name: @keyframe identifier

- animation-duration: in s or ms

- animation-timing-function: easing function

- animation-delay: delay the start of the animation by the time given

- animation-fill-mode: defines how properties from the keyframes are applied to an element before the animation starts or after the animation ends (or both), its value:
  - none: the keyframes are only applied for the duration of the animation

  - forwards: the styles from the last keyframe of the animation remain applied to the element after the animation ends

  - backwards: the styles from the first keyframe are applied during the animation delay period

  - both: you get the effects of forwards and backwards

- animation-iteration-count: how many times the animation runs

- animation-direction:
  - normal
  - reverse
  - alternate: runs the animation forward and then backward
  - alternate-reverse: runs the animation backward, then forward

- animation-play-state: Defines whether or not the animation is currently playing. This could be manipulated with JavaScript to pause and resume an animation: _running_ and _paused_ value

```CSS
/* css animation definition by at-rele*/
/* 'colors' is the @keyframes identifier */
/* 0% can be replaced with 'from' */
/* 100% can be replaced with 'to' */
@keyframes colors {
  0% {
    background: red;
  }
  50% {
    background: blue;
  }
  100% {
    background: green;
  }
}
/* in animation shorthand first time value is always duration and the second is delay */
animation: colors 2s;

animation: color 2s ease-in-out 2s both;

animation: pulse 2s linear infinite;

/* multiple animations for one element */
@keyframes color {
  from {
    background-color: red;
  }
  to {
    background-color: blue;
  }
}

@keyframes spin {
  from {
      transform: rotate(0);
  }
  to {
    transform: rotate(360deg);
  }
}

animation: color 5s alternate infinite,
               spin 1s linear infinite;
```

## Property types

### Layout properties

- affect how an element is laid out on the page like width, heigh, padding, and margin -> most expensive to animate in case of performance

### Paint properties

- affect how an element is painted on the screen like color or background-image -> not so expensive by their animations must be carefully used in mobile devices

### Composite properties

- like transform and opacity -> much cheaper to animate them

- Animations can sometimes be improved by setting the will-change property on an element. This is a hint to the browser that a certain property or properties will be changing due to an animation or transition, so the browser can take that into account when optimizing for the animation (keep animations smooth).

- Overusing will-change can interfere with that optimization and could actually make performance worse. It’s intended more as a last resort to improve performance.

```CSS
will-change: transform, opacity;

/* disabling animation for improving the accessibility */
@media (prefers-reduced-motion: reduce) {
  .loader {
    animation: none;
  }
}
```

## Flexbox (Flexible Box Layout Module)

- a powerful tool for bauilding layouts with CSS, one-dimensional layout (just horizantal or just vertical)

- An element using flexbox as its layout is referred to as a flex container, and the elements inside it are flex items.

### Direction

- defined by flex-direction (container direction) -> row(horizontal) or column(vertical), row-reverse, column-reverse

- A flex container is created by setting an element’s display property to the value flex. This will create a block flex container. You can also create an inline flex container by setting display to inline-flex.

- Related to the direction is the concept of the axis. The main axis points along the direction specified in flex-direction, and the cross axis points perpendicular to it.

- For example, if flex-direction is set to row, the main axis goes horizontally from left to right, and the cross axis goes vertically from top to bottom.

```CSS
/* basic flex layout */
.container {
    display: flex;
    flex-direction: row;
    border: 1px solid black;
}
```

### Flex Container Properties

- when sum of width of flex items > container width -> use flex-wrap

```CSS
.container {
  border: 1px solid black;
  padding: 0.5rem;
  width: 120px;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.item {
  width: 300px; /* 3 * 300 > 120 -> overflow the container so wrap it */
  text-align: center;
  color: white;
  font-size: 2rem;
}
/* 3 items in a column */
<div class="container">
  <div class="item one">Item 1</div>
  <div class="item two">Item 2</div>
  <div class="item three">Item 3</div>
</div>
```

### Flex Item Properties

- By default, if the items are not large enough to fill the container, there will be empty space.

- flex-grow is a relative measure. If all of the items are set to flex-grow: 1, they will all grow equally to fill the space.

```CSS
.container {
  border: 1px solid black;
  padding: 0.5rem;
  width: 500px;
  display: flex;
  flex-direction: row;
}

.item {
  width: 100px; /* 3 * 300 < 500 -> not fill the container */
  text-align: center;
  color: white;
  font-size: 2rem;
  flex-grow: 1;
}

/* 3 items in a row, fill the container */
<div class="container">
  <div class="item one">Item 1</div>
  <div class="item two">Item 2</div>
  <div class="item three">Item 3</div>
</div>

/* if you want item 2 width be twice of the other item's width */
.two {
  flex-grow: 2;
}
```

- We saw earlier that if the flex items exceed the size of the container, the browser will try to shrink them to fit. By default, it will try to shrink all elements evenly. Just like we can control growth with flex-grow, we can also control shrinking with flex-shrink.

- The flex-shrink property specifies the amount of shrinking that can be done to a flex item relative to the other items. This defaults to 1, which is why all of the elements were shrunk evenly.

```CSS
.container {
  border: 1px solid black;
  padding: 0.5rem;
  width: 300px;
  display: flex;
  flex-direction: row;
}

.item {
  width: 200px; /* 3 * 200 > 300 */
  text-align: center;
  color: white;
  font-size: 2rem;
}

/* flex-shrink of item 1 and 3 is 1, by default */
.two {
  flex-shrink: 2;
}

/* 3 items in a row, fill the container */
<div class="container">
  <div class="item one">Item 1</div>
  <div class="item two">Item 2</div>
  <div class="item three">Item 3</div>
</div>
```

- The flex-basis property sets the initial size of a flex item along the main axis before flex-grow and flex-shrink factors are applied.

### Alignement & Spacing

#### The writing mode

- Some of the values for these properties depend on the writing mode. The writing mode is defined by the writing-mode property. This property determines the way block elements are laid out, and how inline elements flow inside them. Furthermore, the way the writing mode behaves depends on the user’s language.

- In some languages, text flows from left to right (LTR); in others, it flows from right to left (RTL). The default value is horizontal-tb. For LTR languages, elements flow from left to right; for RTL languages, elements flow from right to left. Block elements and lines of text flow from top to bottom.

- Other values include vertical-rl and vertical-lr. For these values, elements flow vertically from top to bottom (for LTR) or bottom to top (for RTL). With vertical-rl, block elements and lines of text flow from right to left (for LTR) or left to right (for RTL). Finally, with vertical-lr, block elements and lines of text flow from left to right (for LTR), or right to left (for RTL).

#### Flex Container Properties

- The justify-content property, set on the container, controls how flex items are aligned/spaced along the main axis. By default, this is set to flex-start. This means the items are bunched together at the beginning of the main axis.

- justify-content values:
  - flex-start
  - flex-end
  - center
  - space-between
  - space-around
  - space-evenly

- The align-items property is also set on the container. It controls how flex items are aligned along the cross axis. The default value is stretch, which will stretch items along the cross axis to fill the container’s size, while respecting height and width constraints.

- align-items values:
  - stretch
  - flex-start
  - flex-end
  - center
  - baseline

- When there are multiple rows (or columns in a column flexbox layout), and there is extra space in the cross axis, align-content specifies how this space is distributed. The default is stretch, which, like with align-items, stretches the items along the cross axis.

- align-content values:
  - stretch
  - flex-start
  - flex-end
  - center
  - space-between
  - space-around
  - space-evenly

#### Flex Item Properties

- The align-items property applies the alignment to all of the flex items, but an individual item can specify its own individual alignment that overrides what was set on the container with the align-self property.

### Order

- By default, items are laid out according to two factors:
  - The order they occur in the HTML
  - The value of the flex-direction property

- This ordering can be changed by using the order property on flex items. This property, when set on a flex item, defines the order in which it appears. Multiple flex items can have the same value for the order property. If more than one item has the same order, those items will be laid out in the order they appear in the source HTML.

- The order property only affects the displayed order on screen. It does not affect the order of the elements in other contexts. A screen reader, for example, will read the elements in their source order, not the displayed order.

### Flexbox Example

- Absolute centering: With flexbox, the problem of absolute (horizontal and vertical) centering is easily solved by setting both align-items and justify-content to center.

## Responsive Design

- a technique for designing page layouts so that they are usable on devices with a variety of different screen sizes -> by media query, flexbox, and grid

- In order for a site to look correctly on mobile devices -> add viewport meta tag to head element

```HTML
<!-- tells the browser how to set the page’s dimensions and zoom level -->
<meta name="viewport" content="width=device-width initial-scale=1.0">
```

### Media queries

- defined as an at-rule (@media), sepcifies a medium (all (default), print, screen, speech) and a condition

- media queries are constantly evaluated, not just when the page first loads

```CSS
h1 {
  color: red;
}

@media screen and (max-width: 400px) {
  h1 {
    color: blue;
  }
}

/* applies only when the user’s device is in landscape orientation */
@media (orientation: landscape)

/* if user is using dark mode */
@media (prefers-color-scheme: dark)

/* logical operators supported: and, or, not */
@media screen
  and (min-width: 600px)
  and (orientation: landscape)
```

- The only operator is also supported. Using only assures that a media query’s rules are not applied on older browsers that don’t understand the full query.

- Media queries can also be used to conditionally load an entire style sheet:

```HTML
<link rel="stylesheet"
      href="style.css"
      media="screen">

<link rel="stylesheet"
      href="print.css"
      media="print">
```

### Breakpoints

- the threshold at which a page’s layout will change due to the viewport size with a media query

- instead of targeting specific device -> set breakpoints based on your content

- Some responsive layouts can be achieved without even using media queries. For example, we can use the flex-wrap property on a flex container to automatically wrap elements to the next line if the viewport is too narrow, in order to prevent the need for horizontal scrolling.

### Fluid Typography

- With fluid typography, it’s possible to automatically scale the font size to viewport size without having to use media queries.

- vw unit == 1% of viewport width -> set fontsize by vw

- use clamp function to set max and min for font size

```CSS
/* min, preferred size, max */
font-size: clamp(48px, 4.8vw, 64px);
```

### Responsive Image

```CSS
/* responsive image without any media query */
img {
  max-width: 100%;
  height: auto;
}
```

## CSS Grid

- Flexbox -> one-dimensional layout -> items in a row or in a column

- Grid -> two-dimensional, most powerful layout system in CSS

- grid container -> outer element that contains the grid layout, set _display_ to grid or inline-grid

- grid item -> all grid container direct children (just immediate children are grid items not all descendants)

- grid lines -> dived rows and columns, numbered from left to right starting with 1

- grid tracks -> rows and columns between grid lines, contain grid items

- grid area -> the space enclosed by any four grid lines. It can contain a single cell or multiple cells

- explicit grid: when grid rows and columns are explicitly defined with CSS properties

- If more items are added than are accounted for in the explicit grid, the grid layout creates additional rows and/or columns to fit these extra items. This is the implicit grid.

- fr unit -> introduced by CSS Grid, fractional unit that referes to a fraction of free space

### Basic Grid

- When there is more space than there are columns, with auto-fill, new columns are created which take up space in the container. With auto-fit, however, it instead sizes the items to fit within the available space without adding more columns.

```CSS
.container {
    display: grid;
/* this grid takes 2 item in a row and 2 item in a column (total: 4 items), more added items goes to implicit grid */
    grid-template-columns: 10rem 10rem; /* height of columns - two 10rem column tracks */
    grid-template-rows: 5rem 5rem; /* width of rows - two 5rem row tracks */
    grid-auto-rows: 5rem; /* size of implicit grid rows */
    gap: 5px;
  }

/* A repetitive grid definition */
.container {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-template-rows: 5rem;
}

/* Using the repeat function */
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, 5rem);
}

/* use minimax function to define min and max size of the track */
.container {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-template-rows: repeat(2, minmax(3rem, auto));
  gap: 5px;
  width: 15rem;
}

/* if you don't want to specify the exact number of rows and columns */
/* below container will fit many columns as will fit inot its width */
.container {
    display: grid;
    grid-template-columns: repeat(auto-fill, 5rem);
    grid-template-rows: 5rem;
    grid-auto-rows: 5rem;
    gap: 5px;
  }
```

### Grid Positioning

- default positioning: items are placed automatically, filling each column then each row

```CSS
/* Specifying the row and column for an specific item */
.item1 {
  background: skyblue;
  grid-row: 2;
  grid-column: 3;
}

/* the item is spanning col 3 & 4 */
.item1 {
  background: skyblue;
  grid-row: 2;
  grid-column-start: 3;
  grid-column-end: 5;
}

/* grid-column shorthand (starting grid line/ending line) */
.item1 {
  grid-row: 2;
  grid-column: 3 / 5;
}

/* using span keyword */
.item1 {
  grid-row: 2;
  grid-column: 3 / span 2;
}

/* the item is spanning row 3 & 4 */
.item1 {
  background: skyblue;
  grid-row: 2;
  grid-row-start: 3;
  grid-row-end: 5;
}
```

### Named Grid Lines

```CSS
.container {
  display: grid;
  gap: 5px;
  width: 500px;
  grid-template-rows:
    [header-start] 2rem
    [content-start] 10rem
    [footer-start] 2rem
    [footer-end];
  grid-template-columns:
    [sidebar-start] 5rem
    [content-start] 1fr
    [content-end];
}

.header {
  grid-row: header-start / content-start;
  grid-column: sidebar-start / content-end;
}

.footer {
  grid-column: sidebar-start / content-end;
}
```

### Named Areas

- The areas are defined with the grid-template-areas property. If two adjacent areas have the same name, then an item placed in that area will span those areas.

```CSS
.container {
  display: grid;
  grid-template-rows: 2rem 10rem 2rem;
  grid-template-columns: 5rem 1fr;
  grid-template-areas:
    'header header header'
    'sidebar content content'
    'footer footer footer';
  gap: 5px;
  width: 500px;
}

.header {
  grid-area: header;
}

.footer {
  grid-area: footer;
}
```

### Grid Alignment

- The justify-items property defines how grid items are aligned along the row axis when there is extra space left inside a grid cell. This property is defined on the container and applies to all the items within that container, its values:
  - stretch
  - start
  - end
  - center

- The align-items property defines how grid items are aligned in the opposite direction, along the column axis. Like justify-items, this property is set on the container, its values:
  - stretch
  - start
  - end
  - center

- If the grid rows and/or columns aren’t sized with relative/flexible units like fr, we could end up with empty space in the grid container. If this happens, the justify-content property defines where within the grid container the grid items will be aligned along the row axis, its values:
  - stretch
  - start
  - end
  - center
  - space-around
  - space-evenly
  - space-between

- align-content is like justify-content, only it determines how the grid rows are aligned along the column axis instead of columns along the row axis, its values:
  - stretch
  - start
  - end
  - center
  - space-around
  - space-evenly
  - space-between

- justify-self: Sets the alignment of an item inside its cell along the row axis.

- align-self: Sets the alignment of an item inside its cell along the column axis.

## CSS Methodologies

- BEM (Block Element Modifier): Uses strict naming rules. Each element’s name has a block, element, and modifier. An example of this is form\_\_button--red. In this example form is the block, button is the element, and red is the modifier.

- OOCSS (Object-Oriented CSS): Applies object-oriented principles to CSS. Separates container elements, or “skins,” from content.

- SMACSS (Scalable and Modular Architecture for CSS): Categorizes CSS rules into five categories: base, layout, module, state, and theme.

## Resources

- Modern_CSS_Master_the_Key_Concepts_of_CSS_for_Modern_Web_Development\_\_Joe_Attardi (2020)
