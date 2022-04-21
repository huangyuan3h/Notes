# SCSS vs module css

We have around of comparison between SCSS and module css. &#x20;

As the Bolt platform code is based on SCSS,  in technology selection scss has been chosen.

However, I have another around of research and css module should be the better choice.



### Discussion

If you are working in css area, you would find there are several solution in this area. Such as sass, less,  css-in-js, styled-css, etc. These technology all are trying to solve the same problem which is to reused the css and divided the css into components.



So, if we start the Protool 2.0 from scratch, but not consider the acceptance and learning curve. The css module would be the best choice. Because this one is natively designed to support component level css.&#x20;



### SCSS

In the Component, the styles folder the structure is:

```
styles
 |
 |---base.scss
 |---_en_ZA.scss
 |---_es_MX.scss
```



Let's take `button` component as example, in `_es_MX.scss`&#x20;

```
// default style
$button-default-background-color: $page-background;
$button-default-color: $active-item;
$button-default-disabled-background-color: $active-item;
$button-default-disabled-color: $page-background;

// primary style
$button-primary-background-color: $active-item;
$button-primary-color: $page-background;
$button-primary-disabled-background-color: $button-disable-background-color;
$button-primary-disabled-color: $page-background;

// danger style
$button-danger-background-color: $error-messages;
$button-danger-color: $page-background;
$button-danger-disabled-background-color: $error-messages;
$button-danger-disabled-color: $page-background;

// float button style
$float-button-background: $white;
$float-button-color: $charcoal-gray;

@import 'base';
```

It would override the default color and let look at `base.scss`:

```
// default style
$button-default-background-color: white !default;
$button-default-color: blue !default;
$button-default-disabled-background-color: blue !default;
$button-default-disabled-color: white !default;

// primary style
$button-primary-background-color: blue !default;
$button-primary-color: white !default;
$button-primary-disabled-background-color: blue !default;
$button-primary-disabled-color: white !default;

// danger style
$button-danger-background-color: red !default;
$button-danger-color: white !default;
$button-danger-disabled-background-color: red !default;
$button-danger-disabled-color: white !default;

// float button style
$float-button-background: white !default;
$float-button-color: grey !default;

// common
$shadow-color: black !default;

.Button {
    cursor: pointer;
    border-radius: px(2);
    border-style: solid;
    border-width: px(1);
    padding: px(12) 0; // for override
    margin: 0 px(5);
    @include shadow;

    &.default {
        background-color: $button-default-background-color;
        color: $button-default-color;
        border-color: $button-default-color;

        &:hover:not([disabled]) {
            background-color: $button-default-disabled-background-color;
            color: $button-default-disabled-color;
        }
    }

    &.primary {
        background-color: $button-primary-background-color;
        color: $button-primary-color;
        &:hover:not([disabled]) {
            background-color: $button-primary-disabled-background-color;
            color: $button-primary-disabled-color;
        }
    }

    &.danger {
        background-color: $button-danger-background-color;
        color: $button-danger-color;
        &:hover:not([disabled]) {
            background-color: $button-danger-disabled-background-color;
            color: $button-danger-disabled-color;
        }
    }

    &[disabled], &.disabled {
        opacity: 0.5;
        cursor: unset;
    }
}
```

&#x20;In Base file, it would define both the styles and default color.



For the theme of one site, it would include:

1. basic setting, like em, varibles , animation, border, shadow, normalization
2. functions to control: breakpoints, z-index, ellipsis,&#x20;
3. defined color and typography like:  palette, color mapping, fonts
4. components styles: button, input, labels..



### CSS module

Link: [https://github.com/css-modules/css-modules](https://github.com/css-modules/css-modules)

Since, I don't have too much experience on this part, but the logic should be same.

The only one I need to mention is that, for the webpack configure, the process flow should include the post-css or sass first.











&#x20;
