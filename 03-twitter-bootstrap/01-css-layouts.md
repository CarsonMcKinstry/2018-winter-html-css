CSS Layouts
=====

Up to this point, we have been working with fairly simple websites. A few headings, some text, and some images. Most websites, though, have much more than just that. 

As HTML and the web in general evolved, the need for being able to easily layout information easily became more and more apparent. This gave rise to multiple different ways to create layouts: table layouts, floats, flexbox, and, most recently, CSS grid. 

**note**: Table layouts have gone by the wayside in favor of more modern layout methods, so we won't be covering this.

## Floats

Floats allow you to specify how an element should flow on the page. This can be to the right, the left, or not at all. Anything on the page can be floated, and can be used for positioning images alongside blocks of text, creating columns of text, and even entire page layouts. 

```html

<html>
  <head>
    <style>
    
      img {
        float: left;
      }

    </style>
  </head>
  <body>
  
    <p>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nullam sapien purus, placerat nec semper non, dictum et lorem. Fusce bibendum tellus et est fringilla tempus. Nulla iaculis ac sapien nec sagittis. Morbi ultrices nisl justo, elementum finibus odio vulputate a. Proin auctor convallis elit ac gravida. Nam consequat suscipit dolor at pretium. Integer vitae semper ex. 
      <img src="image.jpg">
    </p>
  
  </body>
</html>


```
### Clearing floats

Clearing floats refers to telling an element what is allowed to float beside it. Not clearing floats can have odd, unintended consequences. 

An example of this is when an element is taller than it's surrounding container. The element will overflow it's container and in general look somewhat odd. 

Because of these issues, you often will see `.clearfix` as a class definition in CSS that uses floats.

Here are two examples:

```css
  .clearfix {
    overflow: auto;
  }
```

This example will resize the containing element of a floated element to the height of the floated element. However, this relies on you having 100% control of both the padding and margin of these elements. Changing them, again, can have unintended consequences.

A better, more modern way to do a `.clearfix` is to use the `::after` pseudo-selector.

```css
  .clearfix::after {
    content: "";
    clear: both;
    display: block; /* or table, this doesn't really matter*/
  }
```

## Flexbox

Flexbox offers us a much better way to layout pages than floats. Flexbox allows us to work much more efficiently with laying out, aligning, and distributing space between elements in a container, even when we don't know those elements' sizes or the size is dynamic.

Oftentimes you will see a main `.container` class, which we can call a `flex-container`. Items within this contianer are called `flex-items`

```css

  .container {
    display: flex; /* required for flex box */

    /* controls the direction of the the flex */
    flex-direction: row | row-reverse | column | column-reverse; 

    /* controls how flex-items distribute on the X-axis */
    justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;

    /* controls how flex-items distribute on the Y-axis on the current line  */
    align-items: flex-start | flex-end | center | base-line | stretch;

    /* controls how rows distribute on the Y-axis */
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;

    /* controls whether or not items wrap to the next line or not */
    flex-wrap: nowrap | wrap | wrap-reverse;
  }

  .item {
    /* controls where the item is in the flow */
    order: <integer>;

    /* gives the ability for an item to grow proportionally to other items */
    flex-grow: <integer>;

    /* think flex-grow, but backwards */
    flex-shrink: <integer>;

    /* defines the default size of the element, before remaining space is distributed */
    flex-basis: <length> | auto;

    /* short hand for grow, shrink, basis*/
    flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]; 

    /* controls the alignment of this one item */
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
  }
```
