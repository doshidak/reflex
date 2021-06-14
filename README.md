# `doshidak/reflex`

**[doshidak](https://github.com/doshidak)'s fork of [leejordan/reflex](https://github.com/leejordan/reflex)**

A lightweight, responsive flexbox grid with cross-browser support, an inline-block fallback, and no polyfills.

* [Documentation](http://reflexgrid.com)
* [Examples](http://reflexgrid.com/docs/examples.html)
* [Original README](https://github.com/leejordan/reflex/blob/master/README.md)
* [Original Repository](https://github.com/leejordan/reflex)

## What's Different?

**tl;dr:** If you solely use CSS, then there's no need to use this fork. Use the official version instead. This fork fixes some SCSS stuff for SCSS-based projects.

### Dart Sass

The SCSS compiler in the original repository made use of [`node-sass-chokidar`](https://github.com/michaelwayman/node-sass-chokidar), which at the time of writing, has a [deprecation warning](https://github.com/michaelwayman/node-sass-chokidar#deprecated) in favor of [`dart-sass`](https://github.com/sass/dart-sass).

`node-sass-chokidar` has been removed as a dependency in lieu of `dart-sass`, in addition to updating all applicable scritps that made use of the former. The compiled CSS in this project was recompiled by the latter.

### Division Deprecation Fix

If your project makes use of Dart Sass (via the [`sass`](https://www.npmjs.com/package/sass) package), you may encounter several warnings that read:

```
DEPRECATION WARNING: Using / for division is deprecated and will be removed in Dart Sass 2.0.0.
Recommendation: math.div($index, $reflex-columns)
```

While these warnings don't affect the runtime functionality, they flood your console, which can get pretty annoying. This fork fixes the deprecations by applying the recommendations.

### `:root` CSS Variables

The original `reflex-grid` adds [CSS variables to the `:root` pseudo-element](./scss/includes/_variables.scss#L60-L73).

These are useful for accessing `reflex-grid` variables in CSS, but for projects solely using SCSS, you may find you'll never use these:

```css
/* css */

.elem {
  max-width: var(--reflex-sm);
}
```

...since you would typically just do this:

```scss
// scss

@import '~reflex-grid/scss/reflex';

.elem {
  max-width: $reflex-sm;
}
```

This fork disables these CSS variables by default, but can be enabled in [the following config variable](./scss/includes/_variables.scss#L57):

```scss
$reflex-enable-css-vars: true;
```

## Installation

```shell
$ yarn add [--dev] doshidak/reflex
```

## Usage

### SCSS

```scss
@import '~reflex-grid/scss/reflex';
```

### JS

```js
import 'reflex-grid/scss/reflex.scss';
```

Or, if you prefer to import the CSS versions instead:

```js
import 'reflex-grid/css/reflex.css';
// OR
import 'reflex-grid/css/reflex.min.css';
```
