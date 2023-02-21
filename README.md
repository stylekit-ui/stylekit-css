# Stylekit CSS

Stylekit CSS is a styling toolkit to facilitate the development of user interfaces.

## Getting started

To use Stylekit CSS, make sure you have the prerequisites installed before continuing on with the installation steps.

### Prerequisites

- [Node](https://nodejs.org/en/download/)
- [Dart Sass](https://sass-lang.com/install)

### Install via clone

Clone Stylekit CSS to the desired directory in your project. Remember that the path to the Stylekit module is affected depending on where you put it in relation to your `index.scss` file. The example below includes Stylekit CSS in the same directory as your `index.scss` file.

1. Clone the repository
   ```sh
   # Change to your desired directory
   cd my-project/styles/

   # Clone the project
   git clone https://github.com/stylekit-ui/stylekit-css
   ```
2. Include the Stylekit module in your `index.scss`
   ```scss
   // index.scss
   @use "stylekit" as *;
   ```
3. Configure Stylekit CSS (optional but recommended)
   ```scss
   // index.scss
   @use "stylekit" as * with (
     $config: (
       theme: (
         breakpoints: (
           md: 40em,
           lg: 80em
         ),
         colors: (
           success: green,
           danger: red
         ),
         spacing: (
           nano: 0.25rem
         )
         ...
       ),
       layouts: (
         wrap: (
           max-width: 100rem
         )
       ),
       ...
     )
   );
   ```
4. Make sure your `index.scss` file compiles with a sass command
   ```js
   // package.json
   {
     "name": "my-project",
     "scripts": {
       "dev": "sass styles/index.scss public/index.css --no-source-map --style expanded",
       "build": "sass styles/index.scss public/index.min.css --no-source-map --style compressed",
       "watch": "npm run dev & npm run dev -- --watch"
     },
     "devDependencies": {
       "sass": "^1.43.2"
     }
   }
   ```  
## Core concepts

Will be updated.

## Layouts

### Flex

Flex handles box alignment and element composition with endless flexibility using one single class and custom properties.

#### Class

`.layout-flex`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--direction` | `row` | `row`, `row-reverse`, `column`, `column-reverse` | `true` | Set the `flex-direction` property.
`--wrap` | `wrap` | `wrap`, `nowrap`, `wrap-reverse` | `true` | Set the `flex-wrap` property.
`--align` | `normal` | `normal`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `align-items` property.
`--place` | `normal` | `normal`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `first baseline`, `last baseline`, `space-between`, `space-evenly`, `space-around` | `true` | Set the `place-content` property, which is a shorthand for the `align-content` and `justify-content` properties.
`--gap` | `0` | `<length>`, `<percentage>` | `true` | Set the `gap` property.
`--width` | `auto` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `auto` | `true` | Set the `width` property.

`.layout-flex > *`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--basis` | `auto` | `<length>`, `<percentage>`, `max-content`, `min-content`, `content`, `auto` | `true` | Set the `flex-basis` property.
`--grow` | `0` | `<number>` | `true` | Set the `flex-grow` property.
`--shrink` | `1` | `<number>` | `true` | Set the `flex-shrink` property.
`--align` | `auto` | `auto`, `normal`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `align-self` property.
`--order` | `0` | `<integer>` | `true` | Set the `order` property.
`--width` | `auto` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `auto` | `true` | Set the `width` property.
`--min-width` | `0` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `auto` | `true` | Set the `min-width` property.
`--max-width` | `none` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `none` | `true` | Set the `max-width` property.

#### Usage

```html
<!-- Align items along the center of the cross axis -->
<div class="layout-flex" style="--align: center;">
  <div>...</div>
  <div>...</div>
</div>

<!-- Align an item along the center of the cross axis -->
<div class="layout-flex">
  <div style="--align: center;">...</div>
  <div>...</div>
</div>

<!-- Pack rows in the center of the cross axis and justify items along the center of the main axis -->
<div class="layout-flex" style="--place: center;">
  <div>...</div>
  <div>...</div>
</div>

<!-- Pack rows at the start of the cross axis and justify items along the center of the main axis -->
<div class="layout-flex" style="--place: flex-start center;">
  <div>...</div>
  <div>...</div>
</div>
```

### Flow

Flow controls vertical spacing between elements within a container. That way we avoid the need to set margins directly on components. Instead, we style the context.

#### Class

`.layout-flow`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--space` | `var(--space-medium)` | `<length>`, `<percentage>`, `auto` | `false` | Set the value for the `--space` variable, which is used to set the `margin-top` property on all child elements except the first one using the adjacent sibling combinator `> * + *`.

#### Usage

```html
<!-- Set a custom space flow between a set of elements -->
<div class="layout-flow" style="--space: 1rem;">
  <div>...</div>
  <div>...</div>
  <div>...</div>
  <div>...</div>
</div>
```

### Frame

Frame embeds a media object with a fixed aspect ratio and with the option to adjust the focus point and fit behavior.

#### Class

`.layout-frame`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--object-x` | `50%` | `<length>`, `<percentage>`, `top`, `right`, `bottom`, `left`, `center` | `true` | Set the x-axis value for the `object-position` property.
`--object-y` | `50%` | `<length>`, `<percentage>`, `top`, `right`, `bottom`, `left`, `center` | `true` | Set the y-axis value for the `object-position` property.
`--object-fit` | `cover` | `contain`, `cover`, `fill`, `none`, `scale-down` | `true` | Set the `object-fit` property.
`--ratio` | `1/1` | `<number>/<number>` (aspect ratio is the specified ratio of `width` / `height`) | `true` | Set the `aspect-ratio` property.

#### Usage

```html
<!-- Display image in 1:1 format -->
<div class="layout-frame">
  <img src="..." alt="..." loading="lazy" />
</div>

<!-- Display image in 16:9 format and change to 5:4 format from the medium breakpoint -->
<div class="layout-frame" style="--ratio: 16/9; --md-ratio: 5/4;">
  <img src="..." alt="..." loading="lazy" />
</div>

<!-- Make sure the image keeps its proportions -->
<div class="layout-frame" style="--object-fit: contain;">
  <img src="..." alt="..." loading="lazy" />
</div>

<!-- Set focus point for the image -->
<div class="layout-frame" style="--object-x: 32%; --object-y: 45%;">
  <img src="..." alt="..." loading="lazy" />
</div>
```

### Grid

Build responsive grid systems with total layout freedom using one single class and custom properties.

#### Class

`.layout-grid`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--columns` | `1` | `<integer>` | `true` | Set the number of columns to use, it is the first parameter of the `repeat()` function used within the `grid-template-columns` property.
`--size` | `1fr` | `<track-list>`, `<auto-track-list>` | `true` | Set the size of each repeated track, it is the second parameter of the `repeat()` function used within the `grid-template-columns` property.
`--align` | `normal` | `normal`, `stretch`, `center`, `start`, `end`, `flex-start`, `flex-end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `align-items` property.
`--justify` | `normal` | `normal`, `stretch`, `center`, `start`, `end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `justify-items` property.
`--place` | `normal` | `normal`, `stretch`, `center`, `start`, `end`, `baseline`, `first baseline`, `last baseline`, `space-between`, `space-evenly`, `space-around` | `true` | Set the `place-content` property, which is a shorthand for the `align-content` and `justify-content` properties.
`--gap` | `0` | `<length>`, `<percentage>` | `true` | Set the `gap` property.
`--width` | `auto` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `auto` | `true` | Set the `width` property.

`.layout-grid > *`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--column` | `auto` | `<custom-ident>`, `<integer>`, `span <integer>`, `auto` | `true` | Set the `grid-column` property.
`--row` | `auto` | `<custom-ident>`, `<integer>`, `span <integer>`, `auto` | `true` | Set the `grid-row` property.
`--align` | `auto` | `auto`, `normal`, `stretch`, `center`, `start`, `end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `align-self` property.
`--justify` | `auto` | `auto`, `normal`, `stretch`, `center`, `start`, `end`, `baseline`, `first baseline`, `last baseline`, `safe center`, `unsafe center` | `true` | Set the `justify-self` property.

#### Usage

```html
<!-- A simple responsive grid from one column to four columns -->
<div
  class="layout-grid"
  style="--columns: 1; --sm-columns: 2; --md-columns: 3; --lg-columns: 4; --gap: 1rem;"
>
  <div>...</div>
  <div>...</div>
  <div>...</div>
  <div>...</div>
</div>

<!-- A responsive grid using auto-fill -->
<div
  class="layout-grid"
  style="--columns: auto-fill; --size: minmax(min(100%, 15rem), 1fr); --gap: 1rem;"
>
  <div>...</div>
  <div>...</div>
  <div>...</div>
  <div>...</div>
</div>
```

### Switch

Switch lets the container space control the behavior of the content by switching from a single column to a multi column layout when the width of the parent element is equal the breakpoint.

#### Class

`.layout-switch`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--breakpoint` | `0` | `<length>` | `false` | Set the breakpoint value for when to trigger the layout switch.
`--columns` | `1` | `<number>` | `false` | Set the number of columns to use when switching to a multi column layout.
`--gap` | `0rem` | `<length>`, `<percentage>` value (needs a unit so the calculation for the `min-width` property does not break) | `false` | Set the `gap` property. The value is also used in a calculation for the `min-width` property used on each column.
`--column-gap` | `undefined` | `<length>`, `<percentage>` (needs a unit, if defined, so the calculation for the `min-width` property does not break) | `false` | Set the `--column-gap` if you need different values for `column-gap` and `row-gap`. `--column-gap` must be the same as the `column-gap` set in the `gap` shorthand property.

`.layout-switch > *`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--column` | `var(--columns)` | `<number>` | `false` | Overwrites `--columns` if, for example, you want different sized columns.
`--grow` | `0` | `<integer>` | `false` | Set the `flex-grow` property.

#### Usage

```html
<!-- Switch to a multi column layout when the parent width is equal to 40rem -->
<div class="layout-switch" style="--columns: 2; --breakpoint: 40rem;">
  <div>...</div>
  <div>...</div>
</div>

<!-- Switch to a multi column layout with different sized columns using a twelve column base -->
<div class="layout-switch" style="--breakpoint: 40rem;">
  <div style="--column: calc(12/5);">...</div>
  <div style="--column: calc(12/7);">...</div>
</div>
```
### Wrap

Wrap creates a responsive wrapping layout that group, pad and align content with the ability to customize it as needed.

#### Class

`.layout-wrap`

Variable | Default | Options | Breakpoints | Description
---|---|---|---|---
`--width` | `calc(100% - var(--padding))` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `auto` | `false` | Set the `width` property. A calc function is used by default to remove the padding from the the width through the `--padding` variable.
`--max-width` | `80rem` | `<length>`, `<percentage>`, `max-content`, `min-content`, `fit-content(<length-percentage>)`, `none` | `false` | Set the `max-width` property.
`--margin-right` | `auto` | `<length>`, `<percentage>`, `auto` | `false` | Set the `object-fit` property.
`--margin-left` | `auto` | `<length>`, `<percentage>`, `auto` | `false` | Set the `spect-ratio` property.
`--padding` | `clamp(2rem, 10vw, 4rem)` | `<length>`, `<percentage>` | `false` | Set the padding value to be used in the calc function for the `--width` variable. A clamp function is used by default.

#### Usage

```html
<!-- Wrap page content with default settings -->
<div class="layout-wrap">
  <header>...</header>
  <main>...</min>
  <footer>...</footer>
</div>

<!-- Wrap an article to a more readable length -->
<div class="layout-wrap" style="--max-width: 40rem;">
  <article>...</article>
</div>

<!-- Wrap an element without padding -->
<div class="layout-wrap" style="--padding: 0;">
  <div>...</div>
</div>
```

## Utilities

Will be updated.
