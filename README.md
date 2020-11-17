# Windy CSS

> CSS Framework written in Stylus inspired by Tailwind and NIB

For websites and webapps there is no way around CSS. It is versatile and powerful, but in some places it is also cumbersome. CSS frameworks make things easier, but sometimes they are already too much. Then there are also functional CSS frameworks like [Tailwind](https://tailwindcss.com/), which put the whole design back into HTML.

Tailwind indeed offers maximum flexibility with attractive results. But it ignores the semantic structure of HTML. Especially if different themes are to be used, the classic approach to separate content and visual design is better.

To get the best of both worlds, I have written functions inspired by Tailwind using the incredibly powerful yet elegant [Stylus CSS preprocessor](https://stylus-lang.com/), which should make the code clearer.

## Get started

First of all windy can be easily installed via npm:

```shell
npm i windy-css
```

We now create a stylus file, e.g. 'mystormy.styl' with the content:

```stylus
@require "windy-css"

// Add your windy CSS styles here :)
```

Now the own file can be translated with Stylus:

```shell
npx stylus -w ./mystormy.styl -o ./mystormy.css -I ./node_modules
```

But also with Webpack etc. it should be possible to integrate Windy in a similar way.

## Units

The units are relative to the font size of the document, which corresponds to '1rem'. Usually these are '16px'. For 'padding' or 'margin' the argument is a pseudo pixel number. So the following class creates a lateral margin of '0.5rem':

```stylus
.demo
  m-x(8)
```

It should always be thought in steps of 8 to get a harmonious picture. Further shortcuts like `p()` or `m-y()` or `p-r()` are available.

## Colors

The colors have also been adopted from Tailwind and can be used beautifully as follows:

```stylus
.success
  color green-900
  background green-100
```

## Breakpoints

Stylus already offers a flexible '@media' support, so it can also be placed within a class or function. The breakpoints are defined as variables. Example:

```stylus
container()
  m-x(32)

  @media lg
    margin-left auto
    margin-right auto
    max-width 960px
```

## Reset

The included reset canonizes all elements so that they are used purely semantically and can be visually overloaded later. The box model is predefined with 'box-sizing: border-box'. In the own CSS definition you should then only set the desired font. 

However, Windy generally does not add styles on its own, so we have to call the following function at the beginning of the CSS file:

```stylus
windy-reset()
```

## Prose

Similar to the reset, there are also predefined styles for continuous text passages, which can be used optionally. For example, for elements within the `.prose` class:

```stylus
.prose
  windy-prose()
```

## Stack Layout

A strong abstraction for the layout, especially for webapps, is provided by stacks. A container can define a vertical `vstack()` or horizontal `hstack()`. The child elements are then arranged accordingly. If an element should consume the remaining space it can be marked with `grow()`. If it should be vertically scrollable, this can be done with `vscroll()`.  If contained content should be placed vertically and horizontally centered, this can be defined with `center()`. In general, the layout is created using a flexbox, so all the usual CSS properties will work.

Example:

```stylus
.app
  hstack()
  
  &_sidebar
    vstack()
        
  &_content
    grow()
    vscroll()
```

## Positioning

But also from the old stylus framework [nib](https://github.com/stylus/nib) I took some things over, like the shortcuts for positioning elements:

```stylus
.header
  absolute top left
  width 100%
```

## File Size

Due to its design Windy is already very economical with definitions. But there is of course more to it: 

1. use [Purge CSS](https://purgecss.com/) to remove unused styles
2. apply a CSS minifier, such as [clean-css](https://github.com/jakubpawlowicz/clean-css)
