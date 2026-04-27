# Tailwind CSS

- **utility-first** CSS framework to _rapidly build modern websites without ever leaving your HTML_

- Nearly all of the basic Tailwind utility classes are thin wrappers around a single CSS style setting, like using m-4 to provide a margin: 1rem or text-lg to change the text size to font-size: 1.125rem.

- The Tailwind code is extremely explicit and makes it possible to understand the display simply by looking at the HTML markup.

## What is Tailwind?

1. a set of utility classes
2. a tool that generates CSS files based on those classes
3. provides _@apply_ directive to compose tailwind classes

### JIT Engine

- Tailwind has a lot of classes -> defining all these potential classes (most of them unused in your project) and sending them to the browser -> performance issue ---> Tailwind uses "just in time engine" to generate only the CSS you are using in your project -> JIT engine has a CLI which can be used by your build tool to generate the CSS

### Installation

```bash
# install tailwind
npm install -D tailwindcss

# create tailwind configuration file (tailwind.config.js)
npx tailwind init
```

- Tailwind CLI uses tailwind.config.js info as input to generate CSS.

```js
// basic tailwind config file for React app
module.exports = {
  // all the files that we might use tailwind classes in them
  content: ["./src/**/*.{html,js,jsx}"],
  theme: {
    extend: {},
  },
  plugins: [],
};
```

- Add tailwind to your CSS files

```CSS
/* index.css */
@tailwind "tailwindcss/base";
@tailwind "tailwindcss/components";
@tailwind "tailwindcss/utilities";
```

## Basics

- Tailwind is made up of many, many small utility CSS class names, most of which set one specific CSS property to one specific value.

- Many CSS frameworks and naming conventions suggest using names that reflect the semantic meaning of the element on the page like button, nav-bar, or menu-item (semantic classes) -> Tailwind classes not semantic at all but has utlity classes like font-bold and m-6 (utility classes)

### Preflight

- _@tailwind base_ contains Tailwind’s reset stylesheet called Preflight. A reset stylesheet is a restyling of all the base HTML elements to a minimal set of styling properties. Without a reset stylesheet, each browser defines its own default set of style properties for how to render individual HTML elements that don’t have further CSS properties. Using a reset stylesheet gives our application control over this baseline, eliminating differences between browsers and providing a more minimal backdrop into which we insert our own custom styling.

- Preflight does a few things:
  - It overrides all styling from headers, so for example, an h1 is visually identical to the base text.

  - It removes styling from ul and ol lists, resulting in no bullets by default, which is an ironic thing to mention in a bulleted list.

  - It sets all margins to zero for elements that would normally have margins.

  - It sets all borders to a 0-pixel width, solid, and the defined border color by default.

  - It gives buttons a default border.

  - It sets images and image-like objects to display: block rather than display: inline.

- _@tailwind components_: quite small, only consists of the definitions of the container CSS classes, which are usually used at the top level of a page to define the box that the whole page is drawn in.

- _@tailwind utilities_: all the utilities and their modified variants

### Duplication Problem

1. define reusable components instead of using same tailwind classes for styling same elements (use title and subtitle component instead of styling h1 every time)

2. use _@apply_ directive

```CSS
/* defining custom selector */
@layer components {
  .title { @apply text-6xl font-bold }
  .subtitle { @apply text-4xl font-semibold }
  .subsubtitle { @apply text-lg font-medium italic }
}

<div class="title">Title</div>

/* defining custom style for an element */
@layer base {
  h1 { @apply text-4xl font-bold }
  h2 { @apply text-2xl font-semibold }
  h3 { @apply text-lg font-medium italic }
}
```

- Using @layer components defines the selector as part of the components and before the utilities. This means if you combine one of our own definitions with a Tailwind utility, the utility wins, which is what we want.

- all the Tailwind utilities have the same specificity

- In Tailwind, if you have two utility classes that define the same property, the one that’s later in the list wins, so class="text-xl text-2xl" will give you text that’s sized 2xl.

- By defining a custom selector inside a layer, the selector is loaded at the end of that layer and before the next layer.

- Firstly @base layer styles are applied, secondly @component and lastly @utilities styles.

### Modifiers

- Tailwind’s way of using CSS pseudo-classes, pseudo-elements, and media queries in the HTML markup

## Typography

- default tailwind font size: 16pt

### Size and Shape (text-{size})

| Class     | Font Size | Line Height |
| --------- | --------- | ----------- |
| text-xs   | 0.75      | 1rem        |
| text-sm   | 0.875rem  | 1.25rem     |
| text-base | 1rem      | 1.5rem      |
| text-lg   | 1.125rem  | 1.75rem     |
| text-xl   | 1.25rem   | 1.75rem     |
| text-2xl  | 1.5rem    | 2rem        |
| text-3xl  | 1.875rem  | 2.25rem     |
| text-4xl  | 2.25rem   | 2.5rem      |
| text-5xl  | 3rem      | 1           |
| text-6xl  | 3.75rem   | 1           |
| text-7xl  | 4.5rem    | 1           |
| text-8xl  | 6rem      | 1           |
| text-9xl  | 8rem      | 1           |

- arbitrary size (both number and unit): text-[20px]

### Styling ({style})

- uppercase
- lowercase
- capitalize
- normal-case

- italic
- not-italic
- no-underline

- below styles have decoration options: decoration-solid, decoration-double, decoration-dotted, decoration-dashed, decoration-wavy

- use decoration-{width}, decoration-auto, decoration-from-font, underline-offset-{width} for the thickness of the line

- use decoration-{color} for line's color
  - underline
  - overline
  - line-through

- 9 grades of boldness: 100 to 900
- normal: 400

- Boldness utility classes:
  - font-hairline
  - font-thin
  - font-light
  - font-normal
  - font-medium
  - font-semibold
  - font-bold
  - font-extrabold
  - font-black

### Color and Opacity

- Tailwind sets 22 different colors by default at 10 different levels, from the lightest at 50 and then every multiple of 100 from 100 to the darkest at 900.
  - text-{color}
  - text-{color}-{level}
  - text-[#xxxxxx]
  - text-{color}-{level}/{opacity} : text-gray-300/20
  - text-{color}-{level}/[arbitrary_value]
  - text-transparent
  - text-inherit (inherit parent's color)
  - text-current (use CSS _currentColor_)

- Colors:
  - Slate, Gray, Zinc, Neutral, Stone
  - Red, Orange, Pink, Rose
  - Amber, Yellow
  - Lime, Green, Emerald, Teal
  - Cyan, Sky, Blue,
  - Indigo, Violet, Purple, Fuchsia

- Opacity:
  - every multiple of 10 between 0 to 100
  - plus 5, 25, 75, 95

- Color of the text pointer:
  - caret-{color}

### Alignment and Spacing

- Horizontal alignment (CSS _text-align_):
  - text-left
  - text-right
  - text-center
  - text-justify

- Vertical alignment (CSS _vertical-align_):
  - align-baseline
  - align-top
  - align-middle
  - align-bottom
  - align-text-top
  - align-text-bottom
  - align-sub
  - align-super

- Line height:
  - leading-none
  - leading-tight
  - leading-snug
  - leading-normal (1.5 tines font size, default)
  - leading-relaxed
  - leading-loose
  - leading-3 to leading-10 (0.75rem to 2.5rem)

- Letter spacing:
  - tracking-tight
  - tracking-tighter
  - tracking-normal
  - tracking-wide
  - tracking-wider
  - tracking-widest

### Special text

- use modifier _selection_ for user selected text styling which will be applied to all the children like: selection:bg-red-400

- use modifier _first-letter_ and _first-line_ for newspaper style effect like first-letter:text-9xl

- Also, Tailwind allows before: and after: as modifiers for the CSS before:: and after:: pseudo-classes, which allow you to insert content that doesn’t show up in the DOM. In most cases, though, it’s easier and more effective to use actual HTML spans to put the content in the right place rather than using the CSS before and after utilities.

### Lists

- styles:
  - list-disc
  - list-decimal
  - list-none

- use list-inside and list-outside for choosing whether the bullet or number is inside or outside.

- use modifier _marker_ for buller/number style like marker:text-blue-300

### Typography Plugin

- legible defaults for basic typography

1. install:

```bash
npm install @tailwindcss/typography
```

2. add to configuration file:

```JS
module.exports = {
  plugins: [
    require('@tailwindcss/typography'),
  ],
}
```

3. add class _prose_

- its size calsses: _prose-sm_, ...
- its color classes: _prose-gray_, _prose-slate_

- A typical use case for the prose plugin is to surround a chunk of previously existing text or rendered markdown. In those cases, the markup inside the prose block will likely have HTML elements that are dynamically generated in such a way where you can’t get to the internal elements of the text. In that case, you can specifically customize the behavior of HTML elements within the prose block. The general pattern here is prose-{element}:{tailwind}, where element is an HTML element (most of your popular HTML elements for prose text will qualify) and tailwind is a Tailwind utility class. An example might be prose-h1:font-bold or prose-a:decoration-red-700. There’s a special element header that matches all the header elements.

### Tailwind Forms

- a better reset styling for froms

```bash
npm install @tailwindcss/forms
```

```JS
module.exports = {
  plugins: [
    require('@tailwindcss/forms'),
  ],
}
```

## The Box

- The difference between invisible and hidden is that a hidden element doesn’t display and also isn’t part of the DOM layout, and so its existence doesn’t affect the layout of other elements. In contrast, an invisible element doesn’t display its contents, but does affect the layout of the rest of the page—it’ll show up as a gap in the page, still sized, but empty.

### Padding

- padding: p{direction}-{size}
- directions value: t, b, l, r, x (horizontal), y (vertical)
- sizes in px:
  0, 0.5, 1, 1.5, 2, 2.5, 3, 3.5, 4, 5, 6, 7, 8, 9, 10, 11, 12, 14, 16, 20, 24, 28, 32, 36, 40, 44, 48, 52, 56, 60, 64, 72, 80, 96

- p-10 == 2.5rem (1/4px==rem)
- px-4 == 1rem
- pt-px == 1px padding top
- p-[15px] -> arbitrary size

### Margin

- margin: m{direction}-{size}
- negative margin: -m{direction}-{size}
- margin size additional value: auto (horizontally centers the element within its parent container)

### Borders (border-{side}-{size})

- the size options for borders are measured in pixels, not rem

- side: b, t, l, r, x, y
- size: 0, 2, 4, 8 (in pixels)
- both side and size are optional
- border-b: 1 pixel bottom border
- border-2: 2 pixels all side border

- styles: border-solid(default), border-dashed, border-dotted, border-double, border-none

- border-{color}: border-gray-500
- border-{color}/{opacity}: border-gray-500/50
- border-r-gray-500: right colored border

- specify single corner for radius with tl, tr, bl, br: rounded-tr-md, rounded-b-full

| Class            | Radius Size     |
| ---------------- | --------------- |
| rounded-none     | 0               |
| rounded-sm       | 0.125rem        |
| rounded          | 0.25rem         |
| rounded-md       | 0.375rem        |
| rounded-lg       | 0.5rem          |
| rounded-xl       | 0.75rem         |
| rounded-2xl      | 1rem            |
| rounded-3xl      | 1.5rem          |
| rounded-full     | infinity        |
| rounded-[{size}] | arbitrary value |

- Rings: another way to define borders, can have width, color, opacity, and an optional offset -> ring-{width}, ring-{color}, ring-{color}/{opacity}, ring-offset-{pixels}, ring-offset-{color}

- ring -> 3 pixels
- ring-inset -> draws the ring in the content part of the box, rather than the border part of the box

### Background Color (bg-{color}/{opacity})

- Box Shadow:
  - shadow: 10% opacity black border that is 1-pixel vetically offset with a 3-pixel width
  - shadow-{color}
  - shadow-{size}: xs, sm, md, lg, xl, 2xl
  - shadow-inner: makes the element look like it’s lower than the rest of the screen
  - shadow-none

- Drop Shadow:
  - the drop shadow will work better if the element is not rectangular
  - drop-shadow-{size}

### Gradients

- bg-gradient-to-{direction}
- direction: t, b, r, l
- bg-gradient-to-t: start from bottom to top
- bg-gradient-to-l: start from right to left
- corner directions for diagonal gradient: tl, tr, bl, br
- bg-gradient-to-tr: diagonally from bottom left to top right
- bg-none
- bg-gradient-to-l from-red-500 to-blue-500 via-yellow-500 : stop at yellow in the middle
- If you specify a “from” or both “from” and “via” without specifying a “to” color, the gradient will shade toward transparent.

### Background Images

- 3 ways:
  1. use _style_ attribute of the element:

  ```HTML
    <div style="background-image: url(whatever)"></div>
  ```

  2. class="[background-image:url({url})]"

  3. define your own CSS utility class:

  ```CSS
    .bg-pattern-image {
      background-image: url(whatever);
    }
  ```

  - bg positioning:
    - bg-center
    - bg-right
    - bg-left
    - bg-top
    - bg-bottom
    - bg-left-top
    - bg-left-bottom
    - bg-right-bottom
    - bg-right-top

  - tiling: if image is smaller than the container
    - bg-repeat
    - bg-repeat-x
    - bg-repeat-y
    - bg-no-repeat
    - bg-repeat-round
    - bg-repeat-space

  - scrolling:
    - bg-fixed
    - bg-local
    - bg-scroll

  - location:
    - bg-clip-padding (default)
    - bg-clip-border
    - bg-clip-content
    - bg-clip-text

### Filters

- blur
- bg-blur (8-pixel blue)
- blur-sm, blur-md, blur-xl, blur-2xl, blur-3xl
- grayscale and grayscale-0 (negate the grayscale)
- sepia and sepia-0
- brightness-{level}, level values: 0, 50, 75, 90, 95, 100, 105, 110, 125, 150, or 200
- contrast-{level}, level values: 0, 50, 75, 100, 125, 150, 200
- saturate-{level}, level values: 0, 50, 100, 150, 200

### Height and Width

- w-{size}
- h-{size}
- w-1/2: 50%
- special size options:
  -auto: auto-sizing
  -px: single pixel
  -full: 100% of the parent container
  -screen: 100% of the viewport
  -min: minimum content size (CSS min-content)
  -max: maximum content size (CSS max-content)
  -fit: fit content size (CSS fit-content)

- min and max height and width:
  - min-h-0
  - min-h-full
  - min-w-0
  - min-w-full
  - min-h-screen
  - max-h-{size}
  - max-h-full, max-h-screen
  - max-w-0
  - max-w-none: no width
  - max-w-{size}: size is from xs(20 rem) to 7xl(80rem)
  - max-w-prose: used for text (65 char side)
  - max-w-screen-sm, max-w-screen-md,max-w-screen-lg, max-w-screen-xl max-w-screen-2xl

## Page Layout

### Containers

- All the container utility does in Tailwind is specify the max-width of the element based on the width of the browser viewport.

- For example, any viewport between 640 and 768 pixels wide would be set to a max-width of 640 pixels. Once the viewport goes over 768, the max-width stays at 768 pixels until the viewport hits 1024 pixels and then jumps again when the viewport reaches 1280 pixels.

- A Tailwind container doesn’t automatically horizontally center its child elements. To get centering behavior, you pair the container with mx-auto. A Tailwind container also doesn’t introduce a padding or margin to pull its elements away from the browser’s border. To get this behavior, you pair the container with an m- or p- utility. So a plausible class list for your top-level element might be class="container mx-auto py-12 px-6".

### Floats and Clears

- In CSS, the float property positions content inside its container. Typically, the float property is used to position a particular element, often an image, to one side or the other of its container, allowing the rest of the container, often text, to stay completely on the other side, rather than mixing the elements together.

- Tailwind provides float-left and float-right for positions, and float-none as a reset option.

- The CSS clear property forces an element to be placed below any elements it might otherwise overlap with on one or both sides. (Technically, it prevents other elements from floating, which amounts to the same thing.) Tailwind provides utilities to specify a clear behavior on either side, both sides, or no sides: clear-left, clear-right, clear-both, and clear-none.

### Position and Z-Index

- z-{index}
- index values: 0, 10, 20, 30, 40, 50, or auto
- -z-{index}: negative

### Tables

- CSS grid is preferable to tables.
- table-auto: keep the default browser behavior of auto spacing the columns of a table based on its content
- use table-fixed on table element for customizable column width and then use w-{size} for each th element

- border-collapse and its reverse is border-separate
- odd: and even: modifiers for rows

### Grids

- grid utility instead of display: grid

- grid-cols-{count}
- count from 1 to 12
- grid-cols-none for reseting
- rows are automatically created based on the number of cols (no need for explicit definition)

- by adding grid-rows-{count} the whole grid twist 90-degree

- You can also specify the direction in which data flows through the grid. The default, grid-flow-row, causes elements inside the grid to flow horizontally in rows, as you saw in the earlier example. This is the normal behavior of DOM elements that you’re probably familiar with. Or you can use grid-flow-col, in which case elements in the grid fill vertically column by column

- you can add a gap between table cells with the conveniently named gap-{size} helper, which takes a suffix that’s the size of the gap, using the same “some numbers from 0 to 96 and also px” measurement scheme we saw for padding and margins. If you want the gap sizing to only be horizontal, you can use gap-x-{size}. And if you want the gap to only be vertical, use gap-y-{size}.

- Using span, you specify the number of columns or rows you want the cell to take up with col-span-{count} or row-span-{count}, where the suffix is the number of columns or rows. The default then is col-span-1 or row-span-1. The reset helpers are col-span-auto and row-span-auto.

```HTML
<div class="grid grid-cols-2 w-1/4 gap-4">
  <div class="border bg-gray-300 text-center">A</div>
  <div class="border bg-gray-300 text-center">B</div>
  <div class="border bg-gray-300 text-center">C</div>
  <div class="border bg-gray-300 text-center">D</div>
</div>
```

- You can adjust the placement of a grid item by specifying its start and end with col-start-{column} and col-end-{column} or row-start-{row} and row-end-{row}, where the suffix is either the number of the location or the reset value, auto. The key points are that the lowest start location is 1 and the end location is exclusive, meaning it’s not part of the item. Declaring an item as class="col-start-2 col-end- 4" means the element will encompass column 2 and column 3, but not column 4.

- By default, the start and end locations are automatically determined by the placement of the previous items in the grid, and the span is 1. You can specify any two of the start, end, and span items, and the layout will work. For example, class="col-span-3, col-end-5" would take up columns 2, 3, and 4, spanning 3 columns and ending before the fifth column.

### Columns

- suitable for magazine/photo layout

- column-{count}: from 1 to 12

or

- column-{size}: from 2xs to xs, sm, md, lg, xl, and then 2xl through 7xl (16rem to 80rem)

- column-auto: reset
- column-[{size}]

### Flexbox

- Grid vs Flexbox
  - A flexbox container has better controls for dynamically managing the size of elements.

  - Although a flexbox container is conceptually a single row, it can be made
    to automatically wrap its contents on the screen when the contents get too wide.

  - Flexbox containers can be nested, meaning you can start with a flexbox row, but elements inside that row could themselves be flexbox columns, which in turn could contain flexbox rows. Nesting flexboxes gives you a
    lot of options for controlling layout.

  - more flexible than a grid and much easier to adapt to different screen sizes

```HTML
<!-- grid -->
<div class="grid grid-cols-3 gap-4 w-1/3">
  <div class="text-center col-span-3">Header</div>
  <div class="text-center w-1/5">Left Sidebar</div>
  <div class="text-center w-3/5">Content</div>
  <div class="text-center w-1/5">Right Sidebar</div>
  <div class="text-center col-span-3">Footer</div>
</div>

<!-- flexbox -->
<div class="flex flex-col w-1/3">
  <div class="flex-grow">Header</div>
  <div class="flex flex-row">
    <div class="text-center w-1/5">Left Sidebar</div>
    <div class="text-center w-3/5">Content</div>
    <div class="text-center w-1/5">Right Sidebar</div>
  </div>
  <div class="flex-grow">Footer</div>
</div>
```

- container: flex utility

- wrapping container: flex-no-wrap(default), flex-wrap, flex-wrap-reverse

- flex direction: flex-row/flex-row-reverse or flex-column/flex-column-reverse

- row direction is based on the text direction (rtl/ltr), but column direction is always top to bottom

- The axis in the direction of the flow is referred to as the main axis, while the other direction is referred to as the cross axis.

- explicitly specify the order of the elements in the flexbox with the order-{integer} utility, where the suffix is any integer from 1 to 12 or use order-first, order-last, order-none

- The “flex” in flexbox comes from the ability of a flexbox container to change the size and placement of its items dynamically.

- basis-{size}: for sepcify flex container element's size (flex-basis property)

- Flex basis specifies the element’s size along the main axis of the flex, meaning width for row boxes, and height for column boxes.

- If a specific width is not specified, a flexbox will grow or shrink the items within it to fill the available space. If you don’t want a specific item to grow or shrink, you specify it as flex-none, which will keep it at its default size.

- If you want the item to be able to grow or shrink as needed to fill the available size of the container, you use flex-auto or flex-1. The difference between the two is that flex-auto starts with each element’s default size and then increases or decreases size for each element that’s able to grow or shrink, whereas flex-1 resets each item to zero size and equally assigns space to all items, regardless of their natural size. In general, using flex-1 on a set of items will give you equally sized items, and flex-auto won’t.

- You can choose to specify shrink behavior without touching grow behavior. To allow shrinking, use flex-shrink, and to prevent shrinking, use flex-shrink-0. Similarly, flex-grow and flex-grow-0 allow and prevent element growth without affecting shrink behavior.

### Box Alignment

- The Tailwind utilities that affect placement along the main axis all start with justify-, and utilities that affect placement across the cross axis don’t.

- Main Axis (justify-{})
  - justify-start places the elements against the beginning of the axis, based on the text direction.

  - justify-end puts the items against the end of the axis.

  - justify-center centers the items—a longstanding CSS frustration.

  - justify-between places the first element against the beginning of the flexbox, the last element against the end of the flexbox, and then even spacing between internal elements. If the flexbox has three items, you get two identically sized spaces with a pattern of AxBxC.

  - justify-evenly places an equal amount of space around each item. If the flexbox has three items, four identically sized spaces are placed around them with a pattern of xAxBxCx.

  - justify-around places identical spacing around each side of each item. In practice, this makes the end spacing less than the internal space because each internal space contains the left space of one element and the right space of the other. If the flexbox has three items, six equally sized spaces are placed around them with a pattern of xAxxBxxCx.

- An element’s placing within its individual box can be controlled with a class on the container, with the options being justify-items-start, justify-items-end, and justify-items-center for placement. If you want the item to expand to fill its space, you’ve got justify-items-stretch, and the reset option is justify-items-auto. Note that you’d normally use either a regular justify- to space items or a justify-items- to space items within it’s box, but you wouldn’t normally need to do both. If a single element of the box wants to override the container’s justification, you can use justify-self-{option} with the same five options that exist for justify-items.

- Cross Axis (content-{})
  - content-start pushes items against the top of a multi-row flexbox, while content-center vertically centers them.

  - items-center vertically centers items along the cross axis. Similarly, the same five options exist for a self override, but the prefix is only self-, as in self-start or self-center.

- you can manage both axes at the same time with the prefixes place-content-, place-items-, and place-self-, with the result equivalent to having done both the main and cross axis spacing. So place-content-center is equivalent to the combined justify-center and content-center, while place-items-start is equivalent to justify-items-start and items-start.

## Animation

- animate-bounce: describes a one-second transition translating the vertical position down by 25% of the size of the element and then back to the original position, so it gives a slight downward bounce

- animate-ping: one-second animation from regular size and opacity to twice the size and 0 opacity, which gives a pretty effective signal pulse effect

- animate-pulse: two-second transition between 0.1 opacity and 0.5, which produces a slight fade effect on the element

- animate-spin: a full rotation of an object 360 degrees in one second like loading status marker

- animate-none: for negation

## Transition

- you’d declare an element to have a class of transition, which causes the element to use transition effects for the CSS properties, background-color, border-color, box-shadow, color, fill, opacity, stroke, and transform

- transition-all: for all properties
- transition-color
- transition-opacity
- transition-shadow
- transition-transform

- duration-{milliseconds}
- delay-{milliseconds}
- milliseconds values: 75, 100, 150, 200, 300, 500, 700, or 1000

- By default, the transition is applied linearly (ease-linear)
- other utilities: ease-in-out, ease-in, ease-out

## Transformation

- scale-{percentage}: 0, 50, 75, 90, 95, 100, 105, 110, 125, and 150
- scale-x-{percentage}
- scale-y-{percentage}

- rotate-{degrees}: 0, 1, 2, 3, 6, 12, 45, 90, and 180
- -rotate-{degrees}: counter-clockwise
- origin-center (default), origin-top, origin-bottom-right, ...

- skew-x-{degrees}
- -skew-x-{degrees}
- skew-y-{degrees}
- -skew-y-{degrees}

- translate-x-{size}
- -translate-x-{size}
- translate-y-{size}
- -translate-y-{size}
- In addition to the number set, you have as suffixes px for a single pixel, full for “move this the exact amount of its size in that dimension,” and 1/2 for “move it half the amount of its size in that dimension,” as in translate-x-full or translate-y-1/2.

- cursor-auto, cursor-default, cursor-move, cursor-not-allowed, cursor-pointer, cursor-text, and cursor-wait.

- allow and disallow text copy:
  - select-none
  - select-text
  - select-all (make the entire text autoselect on click)

- You can also give an element a resize handle with resize, and limit the handle to one direction with resize-x or resize-y, and reset it with reset-none.

## Responsive Design

- Any responsive modifier causes the utility to take effect at the specified screen width or any larger screen width.

- Tailwind utilities define a minimum width to take effect but not a maximum width.

- If no modifier is used, the default minimum width is 0—the utility is always in effect.

- If you define something as being for small screen widths, Tailwind applies that behavior all the way up—small, medium, large, and beyond. If you want behavior only on small screens, you define the small-screen behavior without a modifier and the canceling behavior with a mid-screen or wide-screen modifier.

- The five screen widths are:
  Small (sm:)—640 pixels and up
  Medium (md:)—768 pixels and up
  Large (lg:)—1024 pixels and up
  Extra large (xl:)—1280 pixels and up
  Extra extra large (2xl:)—1536 pixels and up

- the utilities that don’t have modifiers should describe the behavior you see on the smallest screen, and then you bring in modified utilities to adjust behavior as the screen gets bigger. The idea is that you’ll define your design for mobile devices first, and then use the modifiers to adjust the design for larger screens.

- It’s worth mentioning that you can combine screen size with other modifier:md:hover:font-bold lg:hover:font-black is perfectly legal.

- use _hidden_ for hiding elements in small screens and _block_ to show it in the large screen (lg:block)

## Customizing Tailwind

### Configuration File

- The configuration file is optionally generated as part of your Tailwind installation.

- Tailwind considers each family of utilities to be a core plugin; you can see a complete list in the Tailwind documentation. The theme object references these core plugin names to allow you to customize the core plugins—most of the core plugins have customization options.

```bash
# create tailwind config file
npx tailwindcss init

# create tailwind config file with the entire default configs explicitly listed
npx tailwindcss init --full
```

```JS
// minimal configuration file
module.exports = {
  content: [],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

- In the configuration file, the theme object has keys that are the names of each core plugin and values that are the configuration options for that plugin. The three special configuration options, screen, color, and spacing, aren’t core plugins themselves but are the basis for the configuration of many other core plugins.

- For Tailwind, the theme is the entire set of defaults, and there’s only one. If you want to change color schemes, you need to either use CSS variables or use the dark: modifier to specify behavior under dark mode.

- You can customize the theme in two ways: (1) override entire options or (2) extend options.

```JS
// overriding 'screens' with a new set of values, instead of sm: use phone:
theme: {
  screens: {
    'phone': '640px',
    'landscape': '768px',
    'tablet': '1024px',
    'laptop': '1280px',
  }
}

// extending 'screen' by adding a new value
theme: {
  extend: {
    screens: {
      3xl: '2440px',
    }
  }
}

// default screen values
module.exports = {
  theme: {
    screens: {
      'sm': '640px',
      'md': '768px',
      'lg': '1024px',
      'xl': '1280px',
      '2xl': '1536px',
    }
  }
}
```

- If the value you provide for the screen-width keys is a string, it’s considered the min-width of the breakpoint when generating the CSS. You can also pass an object with min and max keys if you want to specify the breakpoints differently. If you only specify max values, then the responsive behavior is reversed. Unmodified utilities apply at the largest size, and modifiers take effect as the screen gets smaller:

```JS
// you can also add min value
module.exports = {
  theme: {
    screens: {
      '2xl': {'max': '9999px'},
      'xl': {'max': '1535px'},
      'lg': {'max': '1023px'},
      'md': {'max': '767px'},
      'sm': {'max': '639px'},
    }
  }
}
```

```JS
// define your own modifier (print:)
module.exports = {
  theme: {
    extend: {
      screens: { 'print': {'raw': 'print'} },
    }
  }
}
```

### Default Colors

```JS
// completely replace your own set of colors
module.exports = {
  theme: {
    colors: {
      gray: colors.warmGray,
      red: colors.red,
      green: colors.green,
    }
  }
}

// just adding your own colors
module.exports = {
  theme: {
    extend: {
      colors: {
        "company-orange": "#ff5715",
        "company-dark-blue": "#323C64",
        "company-gray": "#DADADA",
      }
    }
  }
}

// extending red color with a new level
module.exports = {
  theme: {
    extend: {
      colors: {
        "red": {
          ...colors.red,
          "450": " #CC0000",
        }
      }
    }
  }
}

// enabling dark: modifier
module.exports = {
  darkMode: "media",
}
```

- If darkMode is set to media, then Tailwind uses the prefers-color-scheme media setting of the browser. If you’d rather control the mode setting yourself, you can set darkMode to class, and then Tailwind adds a utility class dark, which changes any element inside that class to dark mode.

### Spacing

```JS
// p-small, p-medium, p-large
module.exports = {
  theme: {
    spacing: {
      'small': 4px,
      'medium': 12px,
      'large': 36px
    }
  }
}
```

- Nearly every Tailwind utility has a series of suffixes off of a base pattern. And nearly all of them allow you to override or extend them the same way you do for spacing and colors.

```JS
module.exports = {
  theme: {
    zIndex: {
      "1": "1",
      "5": "5",
      "1000": "1000"
      "-1": "-1",
      "-5": "-5",
      "-1000": "-1000"
    }
  }
}
```

### Change Generated Classes

- Under normal circumstances, the Tailwind compiler generates CSS only for the class names that are used in your application. However, there are some circumstances under which you might want to modify that configuration.

- The configuration file has a content key that should contain a list of file patterns for any file in your project that might reference a Tailwind utility. This includes your static .html files, but also your .jsx files for a React project or .erb files for a Rails project. It even includes other files that might reference Tailwind utilities that are called by template files. (But don’t include other .css files—you want to list the files that use Tailwind classes, not the files that define Tailwind classes.)

```JS
module.exports = {
  content: [
    "./src/**/*.{html, jsx, tsx}",
  ],
}
```

On the other hand, while the cost of including non-front-end files is small,
the cost of including, say, your entire node-modules directory is high, both in
the time it takes to run the command line tool and in the amount of
unneeded CSS it would generate.
The mechanism Tailwind uses is simple by design. It tries to split the associ-
ated files into individual words and then matches it against a list of Tailwind
patterns to determine which words are potential Tailwind utilities that need
CSS to be generated for them.
This process errs on the side of caution in that it might capture class names
not being used as class names, which is generally fine and a million times
easier than trying to guess in the general case what is a real CSS class and
what is just a line of JavaScript or a comment.
What it won’t catch is a class name that’s dynamically created via string
concatenation.
In Chapter 3, Typography, on page 17, we looked at the following example for
creating a hover effect:

const hoverDarker = (color) => {
return `text-${color}-300 hover:text-${color}-700`
}

This function, because it creates a class name dynamically, would prevent
those classes from being found by Tailwind, so you’d either need to use those
classes elsewhere or find another way to create this feature.
One option would be a safelist. Tailwind provides a configuration key called
safelist that allows you to specify Tailwind classes that you want to guarantee
will be generated. The individual listings in the safelist can be strings or
JavaScript regular expressions, with some limitations:

```JS
module.exports = {
  content: [
    "./app/views/**/*.{html, erb}",
    "./app/helpers/**/*.rb"
  ],
  safelist: [
    "bg-red-300",
    "bg-red-700",
    {
      pattern: /bg-(gray|slate|zinc|neutral|stone)-(300|700)/,
      variants: ["hover"]
    }
  ]
}
```

This configuration file safelists two background colors individually, then
matches all the grayscale ones with the regular expression. The pattern of
the regular expression must start with a Tailwind utility. For example, you
couldn’t match all the places gray is used with +.-gray-+., but you can match
all red background colors and opacities with bg-red-+.\\+.. I also don’t think
you could match, say, box and border with bo+.. (At the very least, it’s probably
a bad idea.) You can’t match modifiers in the safelist pattern, but you can
make sure the modifiers are generated by including html in the list of variants
as part of the configuration
You can also create a block list of core plugins by passing an object to the
corePlugins key of the configuration. The keys of this object are the name of core
plugins you want to eliminate, and the values are all false. You’d only do this
if you wanted to block classes you are actually using for some reason:
module.exports = {
corePlugins: {
flex: false,
flexDirection: false,
flexGrow: false,
flexShrink: false,
flexWrap: false,
}
}
This configuration gets rid of all the flexbox-related tools, though I don’t rec-
ommend doing that. Flexbox is pretty useful.

### Variant Modifiers

We’ve seen variant modifiers in Tailwind like hover and focus, but Tailwind
defines a couple dozen modifier, and the command-line tool only generates
the CSS for modifier combinations you actually use.
In addition to the screen size modifiers sm, md, lg, xl, and 2xl, following is a
partial tour of the Tailwind modifiers:
• active: Applies when the element is active.
• dark: Applies if Tailwind thinks it’s in dark mode.
• first-letter: Applies to the first letter of the text.
• first-line: Applies to the first line of the text.
• hover: Applies when the user is hovering the pointer over the element.
• landscape: Applies if the device is in landscape orientation.
• ltr: Applies for text going left to right.
• marker: Applies to the list marker
• motion-reduce: Applies if the user has enabled reduce motion on the system.
It’s often applied with hover, and you’d often have a motion-reduce and a
motion-safe variant.
• motion-safe: Applies if the user has not enabled reduce motion on the system.
It’s often applied with hover, and you’d often have a motion-reduce and a
motion-safe variant.
• portrait: Applies if the device is in portrait orientation.
• print: Applies for the print media type.
• rtl: Applies for text going right to left.
• selection: Applies to text selected by the user.
• target: Applies if the element ID matches the current URL
• visited: Applies if a link has been visited.
Two group properties work by declaring a parent element with the class group.
These variant properties apply when any element in the parent is targeted,
not only the element in question:
• group-focus: Applies to any child when any child under the parent gets the
focus.
• group-hover: Applies to any child when the parent is hovered over. It’s
enabled by default wherever hover is enabled.
A few properties are applied based on the order of the elements within their
parent. These variants would go on the child element, not the parent element,
and are particularly helpful if your template language is generating an entire
loop:
• empty: Applies if the element has no children.
• even: Applies if the element is an even-number child (second, fourth, sixth,
and so on).
• first: Applies if the element is the first (top-most) child of its parent element.
Also, first-of-type.
• last: Applies if the element is the last (bottom-most) child of its parent
element. Also, last-of-type.
• odd: Applies if the element is an odd-numbered child (first, third, fifth,
and so on).
• only: Applies if the element is an only child, also only-of-type.
A few properties apply to form elements:
• autofill: Applies if the box has been autofilled by the browser.
• checked: Applies if the checkbox or radio button has been checked.
• default: Applies if the element still has its default value.
• disabled: Applies when the element is disabled.

• file: Applies to the button in a file input.
• focus: Applies when the element has focus, as in a text field.
• focus-within: Applies to a parent class when any child inside that parent has
focus.
• indeterminate: Applies if a checkbox or radio button is in the indeterminate
state.
• in-range: Applies if the element’s value is in range, as in a number spinner.
• invalid: Applies if the element has an invalid value.
• out-of-range: Applies if the element’s value is out of range, as in a number
spinner.
• placeholder: Applies to placeholder text.
• placeholder-shown: Applies if the placeholder text is still being shown.
• read-only: Applies if the element is read-only.
• required: Applies if the element is required.
Tailwind also uses before and after to match the ::before and ::after pseudo-
classes.

Integrate with Existing CSS
One problem you might have if you’re using Tailwind in conjunction with a
lot of existing CSS is name conflict. Your existing CSS might already define
hidden, flex-grow, or (admittedly less likely) mx-64. Tailwind gives you a way to
prevent this problem by offering you the ability to put a common prefix in
front of all Tailwind utilities: prefix: "<SOMETHING>". If you declare prefix: "twind",
then all the Tailwind utilities are transformed, so you end up with twind-hidden,
twind-flex-grow, and even twind-mx-64. If you have a modifier, it attaches normally,
as in hover:twind-text-black.
A different problem is that your existing CSS may be set up in such a way
that all the existing CSS selectors have high specificity and thus override all
of the Tailwind utilities. You can get around this with a configuration of
important: true, which adds the CSS marker !important to all the Tailwind utilities,
which should give them precedence over existing CSS. This can have
unwanted side effects if you’re using a lot of different CSS libraries, so be
careful with it.
Some template tools don’t allow you to use the colon (:) character in class
names, making Tailwind’s prefixes illegal. You can specify a separator: option
to choose your own separator, so separator: "--" means prefixes would look like
hover--text-black or lg--m0-4. (I think I like the look of that more than the colon.)

Access Tailwind from JavaScript
You can access Tailwind configuration from JavaScript. This is useful if you
want to use those values to create dynamic behavior in your JavaScript
framework. You might have some kind of custom animation that needs to
respect existing colors or spacing, or who knows what.
Whatever you want to do, Tailwind provides a resolveConfig method that takes
as an argument the Tailwind configuration object and allows you to query
the configuration—the full configuration, not only your overrides in the file:
import resolveConfig from 'tailwindcss/resolveConfig'
import myConfig from './tailwind.config.js'
const tailwindConfig = resolveConfig(myConfig)
tailwindConfig.theme.colors
The resulting object from resolveConfig merges your configuration overrides with
the defaults and provides an object you can query.
Plugins
Tailwind plugins are just snippets of JavaScript that you can define that allow
you to insert your own additional classes, patterns, and prefixes to your
Tailwind app. They are actually simple enough that you can insert them inline
in your Tailwind configuration file.
To start, you need to require the plugin function by putting this line at the top
of your tailwind.config.js file:
const plugin = require("taiwindcss/plugin")
Then, inside the configuration itself, you can call that plugin function. The
argument to plugin is a function.
const plugin = require("taiwindcss/plugin")
module.exports = {
content: ["./html/*.html"],
theme: {
extend: {},
},
plugins: [
plugin(({}) => {
})
],
};

The anonymous function takes one argument, which the previous snippet
has as an empty JavaScript object, {}. The object that is actually passed to
that function has a number of parameters, each of which is a helper function
that you can call in the body of the anonymous function to add Tailwind
features. Typically, you’d use JavaScript destructuring syntax to only capture
the helper functions you want to use.
For example, if you want to add your own variant prefix, one of the helper
functions is addVariant(), and you’d use it like this (this adds some extra ordi-
nals):
const plugin = require("taiwindcss/plugin")
module.exports = {
content: ["./html/*.html"],
theme: {
extend: {},
},
plugins: [
plugin(({ addVariant }) => {
addVariant("second-of-type", "&:nth-of-type(2)")
addVariant("third-of-type", "&:nth-of-type(3)")
})
],
};
The addVariant method takes two arguments: (1) the modifier you want to add,
and (2) the CSS pseudo-class or media type it should convert to.
Similarly, Tailwind provides helper methods for addUtilities, addComponents, and
addBase. The addUtilities method takes two arguments: (1) the name of a new
Tailwind utility you want to add, and (2) a JavaScript object with the CSS
property you want that utility to resolve to, as in addUtilities(".big-bold-text", {font-
size: "1.5rem", font-weight: "700"}). The addComponents helper does the same thing,
but puts the styles in the Tailwind components layer. The addBase helper adds
new styles to the Tailwind base layer, meaning that the first argument is an
HTML selector like h4 rather than a CSS class.
There are also matchUtilities and matchComponents methods that allow you to define
a set of dynamic matchers. Both of these can use a helper method theme to
look up values in the current theme as a way of determining what’s in the
set of dynamic matchers. So, theme("spacing") gives you all the spacing options.
See https://tailwindcss.com/docs/plugins for full documentation.

## Resources

- Modern_CSS_with_Tailwind_Flexible_Styling_Without_the_Fuss\_\_Noel_Rappin.pdf (2022)
