# SVG/Palette/Typography

What's the problem when cooperate with the designer?&#x20;

**They always give random icon , colors or fonts.**

To solve this problem, the process flow and management tools has been established for protool team.



### SVG

The package is called `svgr/webpack` [https://www.npmjs.com/package/@svgr/webpack](https://www.npmjs.com/package/@svgr/webpack)

in webpack, the config would looks like:



```
    config.module.rules.push({
        test: /\.svg$/,
        use: [
            {
                loader: '@svgr/webpack',
                options: {
                    native: false, // check for react-native
                    icon: true, // Replace SVG "width" and "height" value by "1em" in order to make SVG size inherits from text size
                    dimensions: false, // Remove width and height from root SVG tag
                    svgo: true, // Use SVGO to optimize SVG code before transforming it into a component.
                },
            },
        ],
    });
```

You may found lots of icon packages could be found in npm or github. The structure is of design the icon structure and mange icon packages is also need to be considered.

One of the example package is : [https://github.com/ant-design/ant-design-icons](https://github.com/ant-design/ant-design-icons)

It would be better abstract the icon into a sub-module of Lerna&#x20;

### Palette

If you find sometimes the border color is `#dddddd` or sometimes is `#747474`

So developer and designer has around of discussion about the issue to have different color used in same component:

```css
// color define for viva site

// Primary Color Palette
$white: #ffffff; // First Level page background color
$light-grey: #fafafa; // Navigation background color.
$white-smoke: #f8f8f8; // description toolbar
$silver-grey: #f4f4f4; // Second Level Page background color.
$medium-gray: #d4d4d4; // Used for Borders & Dividers.
$dark-grey: #747474; // Used for secondary text color. Major section dividers
$charcoal-gray: #333333; // Used for principal text color, overlay header background. non-button based icons.
$light-blue: #1e98d5; // Used for links, active elements, button colors, button based icons, Secondary Level Page Header bgd color
$tangerine: #ff9800; // Used for special CTA’s and special design elements / call outs, and medium “quality” warnings

// Secondary Color Palette
$bright-blue: #196ed2; // Used for special design elements / call outs
$green: #87bc1c; // Used for special design elements / call outs, success messages, PAF Tooltips
$canary: #f8c300; // Used for special design elements / call outs
$red: #ce3438; // Used for Error Messages and poor “quality” warnings
$black: #000; // Used for background screen when overlay / tooltips appear
$concrete-grey: #999999; // Used for Form Field Borders

// the third color palette (found in design but not in palette file)
$denim: #166a93; // button disable color
$seablue: #1c9ad6; // border color for upload icon
$gainsboro: #d8d8d8; // border color for photo list
$grey: #7f7f7f;
$zambezi: #606060;
$summer-sky: #43a0de;
$whisper: #eeeeee;
$alabaster: #f7f7f7;

// the color for loading icon
$curious-blue: #418dc8;
$tangerine-yellow: #f9ca00;
$rio-grande: #b4c624;
$venetian-red: #dd0b15;
```

This is the finally color and defined for all the site, so all the site would just use the color it defined here. Actually it is still too much.



Another good way is to define the component before developing.



### Typography

Have you find the similar component use different font?



![](<../../.gitbook/assets/image (7).png>)

In our storybook, there is a page to display all the font and which place to use these icon.

And in the code, these fonts are abstract to mixin or class and in the css file, it is not allow to define font code. which avoid the conflict.&#x20;









