---
# layout: note_tutorial
title: A Guide to CSS Flex & Grid
catalog: true
tags: 
  - css
permalink: css_layout_flex_grid.html
folder: frontEnd
summary: 
# sidebar: frontEnd_sidebar
# topnav: topnav
---

## Pre-knowledge

> ![MAIN AXIS vs CROSS AXIS](https://user-gold-cdn.xitu.io/2019/8/13/16c884e33c26dbeb?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
> 
> Retrieved from [THIS PAGE](https://juejin.im/entry/6844903911690600456)

## Purpose

Get width/height/order of items (children) to suit the container (parent).

## Features

- Direction-agnostic  

## Scopes of Use

- **Flex**: Best fit applications and small-scale layouts

- **Grid**: Coming in handy for large-scale layouts

## Properties for Parents

### `display`

Defines a flex container, enabling a flex context for all its direct children.

values: 

- `flex`

- `inline-flex`

```html
.conotainer {
  display: flex | inline-flex
}
```

### `flex-direction`

Controls the items to flow horizontally or vertically.

```html
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

- row: left to right in ltr; right to left in rtl  
- row-reverse: right to left in ltr; left to right in rtl  
- column: top to bottom  
- column-reverse: bottom to up  

### `flex-wrap`

Breaks with the convention that restricts items to subsist within one line, whether horizontally or vertically. This property enables items to wrap when necessary.

```html
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

wrap: flex items will wrap onto multiple lines, from top to bottom  
wrap-reverse: flex items will wrap onto multiple lines, from bottom top

### `flex-flow`

A shorthand for the `flex-direction` and `flex-wrap` properties. The default value is `row nowrap`.

```html
.container {
  flex-flow: column wrap;
}
```

### `justify-content`

[EXAMPLE](https://codepen.io/uufishtxl/pen/XWdZjRM)

Defines the alignment of the items along the given axis. This helps to portion out extra space leftover.

```html
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}
```
Align items along the main axis.

However, browser support for these values is nuanced. To ensure your page displays as desired, avail of the safe options only, namely `flex-start`, `flex-end` and `center`.

### `align-items`

[EXAMPLE](https://codepen.io/uufishtxl/pen/XWdZjRM)

Align the items along the cross axis.

### `align-content`

Align the items dispersed in no less than two lines along the cross axis, if there's leftover space along the cross axis.

[EXAMPLE](https://codepen.io/uufishtxl/pen/ExKQNjR)

## Properties for Children (Items)

### `order`

```html
.item {
  order: 5; /* default is 0 */
}
```

[EXAMPLE](https://codepen.io/uufishtxl/pen/jOqZQxQ)

As the number increases, the priority goes down.

### `flex-grow`

Defines the ability of a flex item to grow if necessary.

[EXAMPLE](https://codepen.io/uufishtxl/pen/zYqRMLx)

### `flex-shrink`

Defines the ability of a flex item to shrink if necessary.

When the container is not large enough to accommodate all its children, the latter ones default to shrink by the same proportion to suit themselves. However, you may define a scale specifically for a flex item to let it shrink to a different size. Negative numbers are invalid here.

[EXAMPLE](https://codepen.io/uufishtxl/pen/mdPXQQq)

### `flex-basis`

`flex-basis` is much like `width`. When they co-exist, `flex-basis` prevails over the other. 

> 如果flex-basis和width其中有一个是auto，那么另外一个非auto的属性优先级会更高。
> 
> [RETRIEVED HERE](https://zhoon.github.io/css3/2014/08/23/flex.html)

### `flex`

A shorthand for `flex-grow`, `flex-shrink` and `flex-basis`. The shorthand is recommended rather than separate configurations for three independent properties. Note that the second and third parameters are optional.

### `align-self`

Overrides the default alignment dependent upon the `align-items` configuration on the parent element.

[EXAMPLE]()


The free space is calculated after any non-flexible items.

Repeating the name of a grid area causes the content to span those cells. 


Set a column to be 1fr, but shrink no further than 200px
grid-template-columns: 1fr minmax(200px, 1fr);

There is repeat() function, which saves some typing, like making 10 columns:
grid-template-columns: repeat(10, 1fr);

If no end line value is declared, the item will span 1 track by default.