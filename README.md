# Stylekit CSS

Stylekit CSS is a toolkit that facilitate your development of user interfaces.

## Get started

To use Stylekit CSS, make sure you have the prerequisites installed before continuing on with the installation steps.

### Prerequisites

- [Node](https://nodejs.org/en/download/)
- [Dart Sass](https://sass-lang.com/install)

### Load path

Make sure you update the `--load-path` configuration in your `package.json` file to ensure that Sass can locate the Stylekit module correctly. For additional details on configuring load paths, visit [Dart Sass CLI](https://sass-lang.com/documentation/cli/dart-sass/#load-path).

#### Load path example

In the following example, the system initially searches for the Stylekit module within the `node_modules` directory. If it's not located there, it will continue its search in the root directory `./`. If you have a specific custom path, you can include it using the following format: `--load-path=./custom-path`.

```json
"scripts": {
  "dev": "sass --load-path=./node_modules/stylekit-css --load-path=./ --load-path=./custom-path index.scss dist/stylekit.css --no-source-map --style expanded --watch"
},
```

### Install via NPM

Install Stylekit CSS as a dependency.

```sh
npm install stylekit-css
```

### Install via clone

Clone the Stylekit CSS repository to your preferred directory within your project.

```sh
# Change to your desired directory
cd my-project/styles/

# Clone the project
git clone https://github.com/stylekit-ui/stylekit-css
```

### Compile and watch your styles

Stylekit CSS comes with two ready-made script commands, one for development and one for production. The provided script commands assume that you write and import your code into `index.scss` in the `stylekit-css` folder. Of course, it's possible and recommended, to develop with Stylekit from a different location; just remember to ensure the correct `--load-path`, the source for your primary styling file, and where the built files should be placed. See load path example above for a working script command.

```sh
# Development mode
npm run stylekit:dev

# Production mode
npm run stylekit:build
```

### Add your compiled styles

```html
<link rel="stylesheet" href="stylekit-css/dist/stylekit.css" />
```

The compiled styling file and its path may vary based on your build script.

## Configuration

### Include and configure the Stylekit module in your main stylesheet file

```scss
// index.scss
@use "stylekit" as * with (
  $config: (
    theme: (
      breakpoints: (
        md: 800px,
        lg: 1600px
      ),
      extend: (
        colors: (
          success: green,
          danger: red
          ),
        spacing: (
          xxs: 0.25rem
        )
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

### Extend the Stylekit module with your own utilities and variables

```scss
// index.scss
@use "stylekit" as * with (
  $config: (
    theme: (...),
    layouts: (...),
    utilities: (
      radius: (
        shorthand: radius,
        variable: radius,
        properties: (border-radius),
        variants: (
          sm: 0.125rem,
          md: 1rem,
          lg: 2rem
        )
      ),
      // Utility using multiple properties
      border-block: (
        shorthand: border-block,
        variants: (
          black: (
            border-block-style: solid,
            border-block-width: 1px,
            border-block-color: var(--color-black)
          )
        )
      )
    ),
    variables: (
      radius: (
        variable: radius,
        variants: (
          sm: 0.125rem,
          md: 1rem,
          lg: 2rem
        )
      )
    )
  )
);
```

The above example will result in the following CSS code:

```css
:root {
  --radius-sm: 0.125rem;
  --radius-md: 1rem;
  --radius-lg: 2rem;
}

.radius-sm {
  border-radius: var(--radius-sm);
}

.radius-md {
  border-radius: var(--radius-md);
}

.radius-lg {
  border-radius: var(--radius-lg);
}

.border-block-black {
  border-block-style: solid;
  border-block-width: 1px;
  border-block-color: var(--color-black);
}
```