# CSS Coding Guidelines

This is mostly copied from this fantastic post
> https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06

and merged with this second fantastic ideas
> http://cssguidelin.es/

Naming conventions are adapted from the work being done in the SUIT CSS framework. Which is to say, it relies on _structured class names_ and _meaningful hyphens_ (i.e., not using hyphens merely to separate words).

This is to help work around the current limits of applying CSS to the DOM (i.e., the lack of style encapsulation) and to better communicate the relationships between classes.


**Table of contents**

* [JavaScript](#javascript)
* [Utilities](#utilities)
  * [u-utilityName](#u-utilityName)
* [Components](#components)
  * [componentName](#componentName)
  * [componentName--modifierName](#componentName--modifierName)
  * [componentName__descendantName](#componentName__descendantName)
  * [componentName.is-stateOfComponent](#is-stateOfComponent)
  * [componentName.has-anyOtherComponent](#has-anyOtherComponent)
* [Variables](#variables)
  * [Basic Scales](#basicScales)
  * [colors](#colors)
  * [z-index](#zindex)
  * [font-weight](#fontweight)
* [Polyfills](#polyfills)
* [Formatting](#formatting)
  * [Table of Contents](#tableOfContents)
  * [Titles](#titles)
  * [Quotes](#quotes)
* [Performance](#performance)
  * [Specificity](#specificity)
* [Reusability](#resusability)
  * [Selector Intent](#selectorIntent)
  * [Location Independence](#locationIndependence)
  * [Naming](#naming)


<a name="javascript"></a>
## JavaScript

syntax: `js-<targetName>`

JavaScript-specific classes reduce the risk that changing the structure or theme of components will inadvertently affect any required JavaScript behaviour and complex functionality. It is not neccesarry to use them in every case, just think of them as a tool in your utility belt. If you are creating a class, which you dont intend to use for styling, but instead only as a selector in JavaScript, you should probably be adding the `js-` prefix. In practice this looks like this:

```html
<a href="/login" class="btn btn-primary js-login"></a>
```

**Again, JavaScript-specific classes should not, under any circumstances, be styled.**

<a name="utilities"></a>
## Utilities

Medium's utility classes are low-level structural and positional traits. Utilities can be applied directly to any element; multiple utilities can be used together; and utilities can be used alongside component classes.

Utilities exist because certain CSS properties and patterns are used frequently. For example: floats, containing floats, vertical alignment, text truncation. Relying on utilities can help to reduce repetition and provide consistent implementations. They also act as a philosophical alternative to functional (i.e. non-polyfill) mixins.


```html
<div class="u-clearfix">
  <p class="u-textTruncate">{$text}</p>
  <img class="u-pullLeft" src="{$src}" alt="">
  <img class="u-pullLeft" src="{$src}" alt="">
  <img class="u-pullLeft" src="{$src}" alt="">
</div>
```

<a name="u-utilityName"></a>
### u-utilityName

Syntax: `u-<utilityName>`

Utilities must use a camel case name, prefixed with a `u` namespace. What follows is an example of how various utilities can be used to create a simple structure within a component.

```html
<div class="u-clearfix">
  <a class="u-pullLeft" href="{$url}">
    <img class="u-block" src="{$src}" alt="">
  </a>
  <p class="u-sizeFill u-textBreak">
    â€¦
  </p>
</div>
```

<a name="components"></a>
## Components

Syntax: `<componentName>[--modifierName|__descendantName]`

We use "--" and "__" to obviously separate modifiers from descendant all other syntax variations.

Component driven development offers several benefits when reading and writing HTML and CSS:

* It helps to distinguish between the classes for the root of the component, descendant elements, and modifications.
* It keeps the specificity of selectors low.
* It helps to decouple presentation semantics from document semantics.
* It helps to create location independent classes, which in turn helps creating reusable classes

You can think of components as custom elements that enclose specific semantics, styling, and behaviour.


<a name="componentName"></a>
### ComponentName

The component's name must be written in camel case.

```css
.myComponent { ... }
```

```html
<article class="myComponent">
  ...
</article>
```

<a name="componentName--modifierName"></a>
### componentName--modifierName

A component modifier is a class that modifies the presentation of the base component in some form. Modifier names must be written in camel case and be separated from the component name by two hyphens. The class should be included in the HTML _in addition_ to the base component class.

```css
/* Core button */
.btn {  }
/* Default button style */
.btn--default {  }
```

```html
<button class="btn btn--primary">...</button>
```
<a name="componentName__descendantName"></a>
### componentName__descendantName

A component descendant is a class that is attached to a descendant node of a component. It's responsible for applying presentation directly to the descendant on behalf of a particular component. Descendant names must be written in camel case.

```html
<article class="tweet">
  <header class="tweet__header">
    <img class="tweet__avatar" src="{$src}" alt="{$alt}">
    ...
  </header>
  <div class="tweet__body">
    ...
  </div>
</article>
```

<a name="is-stateOfComponent"></a>
### componentName.is-stateOfComponent

Use `is-stateName` for state-based modifications of components. The state name must be Camel case. **Never style these classes directly; they should always be used as an adjoining class.**

JS can add/remove these classes. This means that the same state names can be used in multiple contexts, but every component must define its own styles for the state (as they are scoped to the component).

```css
.tweet { ... }
.tweet.is-expanded { ... }
```

```html
<article class="tweet is-expanded">
  ...
</article>
```


<a name="has-anyOtherComponent"></a>
### componentName.has-anyOtherComponent

Use `has-otherComponentName` for content-based modifications of components. The component name must be Camel case. **Never style these classes directly; they should always be used as an adjoining class.**

This way you can style components in dependence of existing other components that might or might not
live inside this component. In some cases you want this component react a little bit else if another specific
component is present inside.

JS can add/remove these classes. This means that the same state names can be used in multiple contexts, but every component must define its own styles for the state (as they are scoped to the component).

```css
.tweet { ... }
.tweet.has-btnAtBottom { ... }
```

```html
<article class="tweet has-btnAtBottom">
  ...
  <button class="btn btnAtBottom">Like</button>
</article>
```

<a name="variables"></a>
## Variables

Syntax: `<property>-<value>[--componentName]`

Variable names in our CSS are also strictly structured. This syntax provides strong associations between property, use, and component.

The following variable defintion is a color property, with the value grayLight, for use with the highlightMenu component.

```CSS
@color-grayLight--highlightMenu: rgb(51, 51, 50);
```

<a name="basicScales"></a>
### Basic Scales

It is advisably to create sets of basic variables of scales like:

```CSS
ex:

@fontSize-micro     = 8px;
@fontSize-smallest  = ...
@fontSize-smaller
@fontSize-small
@fontSize-base
@fontSize-large
@fontSize-larger
@fontSize-largest
@fontSize-jumbo
```

You can do this for several properties like:
- colors
- z-index
- font-weight
- line-height
- letter-spacing
- etc.


<a name="colors"></a>
### Colors

All colors should live with there own variables.

When adding a color variable, using RGB and RGBA color units are preferred over hex, named, HSL, or HSLA values.

**Right:**
```css
rgb(50, 50, 50);
rgba(50, 50, 50, 0.2);
```

**Wrong:**
```css
#FFF;
#FFFFFF;
white;
hsl(120, 100%, 50%);
hsla(120, 100%, 50%, 1);
```

<a name="zindex"></a>
### z-index scale

Please use a z-index scale.

`@zIndex-1 - @zIndex-9` are provided. Nothing should be higher then `@zIndex-9`.


<a name="fontweight"></a>
### Font Weight

With the additional support of web fonts `font-weight` plays a more important role than it once did. Different font weights will render typefaces specifically created for that weight, unlike the old days where `bold` could be just an algorithm to fatten a typeface. Obvious uses the numerical value of `font-weight` to enable the best representation of a typeface. The following table is a guide:

Raw font weights should be avoided. Instead, use the appropriate font mixin: `.font-sansI7, .font-sansN7, etc.`

The suffix defines the weight and style:

```CSS
N = normal
I = italic
4 = normal font-weight
7 = bold font-weight
```

See [Mozilla Developer Network ...” font-weight](https://developer.mozilla.org/en/CSS/font-weight) for further reading.


<a name="polyfills"></a>
## Polyfills

mixin syntax: `m-<propertyName>`

Use mixins to generate polyfills for browser prefixed properties.


An example of a border radius mixin:

```css
.m-borderRadius(@radius) {
  -webkit-border-radius: @radius;
     -moz-border-radius: @radius;
          border-radius: @radius;
}
```


<a name="formatting"></a>
## Formatting

The following are some high level page formatting style rules.

<a name="tableOfContents"></a>
### Table of Contents

A table of contents is a fairly substantial maintenance overhead,
but the benefits it brings far outweigh any costs.
A simple table of contents will—in order, naturally—simply
provide the name of the section and a brief summary
of what it is and does, for example:

```css
/**
 * CONTENTS
 *
 * SETTINGS
 * Global...............Globally-available variables and config.
 *
 * TOOLS
 * Mixins...............Useful mixins.
 *
 * GENERIC
 * Normalize.css........A level playing field.
 * Box-sizing...........Better default `box-sizing`.
 *
 * BASE
 * Headings.............H1–H6 styles.
 *
 * OBJECTS
 * Wrappers.............Wrapping and constraining elements.
 *
 * COMPONENTS
 * Page-head............The main page header.
 * Page-foot............The main page footer.
 * Buttons..............Button elements.
 *
 * TRUMPS
 * Text.................Text helpers.
 */
```

<a name="titles"></a>
### Titles

```css
/*------------------------------------*\
    #SECTION-TITLE
\*------------------------------------*/

.selector {}
```

<a name="indenting"></a>
### Indenting

As well as intending individual declarations, indent entire related
rulesets to signal their relation to one another, for example:

```css
.foo {}

    .foo__bar {}

        .foo__baz {}
```

<a name="quotes"></a>
### Quotes

Quotes are optional in CSS and LESS. We use double quotes as it is visually clearer that the string is not a selector or a style property.

**Right:**
```css
background-image: url("/img/you.jpg");
font-family: "Helvetica Neue Light", "Helvetica Neue", Helvetica, Arial;
```

**Wrong:**
```css
background-image: url(/img/you.jpg);
font-family: Helvetica Neue Light, Helvetica Neue, Helvetica, Arial;
```

<a name="performance"></a>
## Performance

<a name="specificity"></a>
### Specificity

Although in the name (cascading style sheets) cascading can introduce unnecessary performance overhead for applying styles. Take the following example:

```css
ul.user__list li span a:hover { color: red; }
```

Styles are resolved during the renderer's layout pass. The selectors are
resolved right to left, exiting when it has been detected the selector does
not match. Therefore, in this example every a tag has to be inspected to see
 if it resides inside a span and a list. As you can imagine this requires
 a lot of DOM walking and and for large documents can cause a significant
 increase in the layout time. For further reading checkout:
 https://developers.google.com/speed/docs/best-practices/rendering#UseEfficientCSSSelectors

If we know we want to give all `a` elements inside the `.user__list` red on
hover we can simplify this style to:

```css
.user__list > a:hover {
  color: red;
}
```

If we want to only style specific `a` elements inside `.user__list` we can
give them a specific class:

```css
.user__list > .link--primary:hover {
  color: red;
}
```

<a name="resusability"></a>
## Resusability

The following sections provides much more zen like suggestions then easy
to follow guide lines. This is just a try to sensitize programmers for
more intention and thinking when writing css.

<a name="selectorIntent"></a>
### Selector Intent

It is important when writing CSS that we scope our selectors correctly,
and that we’re selecting the right things for the right reasons.
Selector Intent is the process of deciding and defining what you want
to style and how you will go about selecting it. For example, if you are
wanting to style your website’s main navigation menu, a selector like this
would be incredibly unwise:

```css
header ul {}
```

This selector’s intent is to style any ul inside any header element,
whereas our intent was to style the site’s main navigation. This is poor
Selector Intent: you can have any number of header elements on a page,
and they in turn can house any number of uls, so a selector like this
runs the risk of applying very specific styling to a very wide number of
elements. This will result in having to write more CSS to undo the
greedy nature of such a selector.

A better approach would be a selector like:

```css
.site-nav {}
```

**Your selectors should be as explicit and well reasoned as your reason for
wanting to select something**

**If a selector will work without it being nested then do not nest it**

<a name="locationIndependence"></a>
### Location Independence

Given the ever-changing nature of most UI projects, and the move to more
component-based architectures, it is in our interests not to style things
based on where they are, but on what they are. That is to say, our components’
styling should not be reliant upon where we place them—they should remain
entirely location independent.

Let’s take an example of a call-to-action button that we have chosen to
style via the following selector:

```css
.promo a {}
```

Not only does this have poor Selector Intent—it will greedily style any
and every link inside of a .promo to look like a button—it is also pretty
wasteful as a result of being so locationally dependent: we can’t reuse
that button with its correct styling outside of .promo because it is explicitly
tied to that location. A far better selector would have been:

```css
.btn {}
```

This single class can be reused anywhere outside of .promo and will always
carry its correct styling. As a result of a better selector, this piece of
UI is more portable, more recyclable, doesn’t have any dependencies, and
has much better Selector Intent. A component shouldn’t have to live in a
certain place to look a certain way.

<a name="naming"></a>
### Naming

As Phil Karlton once said, There are only two hard things in Computer Science:
cache invalidation and naming things.

I won’t comment on the former claim here, but the latter has plagued me for
years. My advice with regard to naming things in CSS is to pick a name that
is sensible, but somewhat ambiguous: aim for high reusability. For example,
instead of a class like .site-nav, choose something like .primary-nav;
rather than .footer-links, favour a class like .sub-links.

The differences in these names is that the first of each two examples is
tied to a very specific use case: they can only be used as the site’s
navigation or the footer’s links respectively. By using slightly more
ambiguous names, we can increase our ability to reuse these components
in different circumstances.

To quote Nicolas Gallagher:

Tying your class name semantics tightly to the nature of the content
has already reduced the ability of your architecture to scale or be easily
put to use by other developers.
That is to say, we should use sensible names—classes like .border or .red
are never advisable—but we should avoid using classes which describe the
exact nature of the content and/or its use cases. Using a class name to
describe content is redundant because content describes itself.

The debate surrounding semantics has raged for years, but it is important
that we adopt a more pragmatic, sensible approach to naming things in order
to work more efficiently and effectively. Instead of focussing on ‘semantics’,
look more closely at sensibility and longevity—choose names based on ease of
maintenance, not for their perceived meaning.

Name things for people; they’re the only things that actually read your
classes (everything else merely matches them). Once again, it is better to
strive for reusable, recyclable classes rather than writing for specific
use cases. Let’s take an example:

```css
/**
 * Runs the risk of becoming out of date; not very maintainable.
 */
.blue {
    color: blue;
}

/**
 * Depends on location in order to be rendered properly.
 */
.header span {
    color: blue;
}

/**
 * Too specific; limits our ability to reuse.
 */
.header-color {
    color: blue;
}

/**
 * Nicely abstracted, very portable, doesn’t risk becoming out of date.
 */
.highlight-color {
    color: blue;
}
```

It is important to strike a balance between names that do not literally
describe the style that the class brings, but also ones that do not explicitly
describe specific use cases. Instead of .home-page-panel, choose .masthead;
instead of .site-nav, favour .primary-nav; instead of .btn-login,
opt for .btn-primary.