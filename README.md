# Css layouts: from float to flexbox and grid

My notes for [LinkedIn Course](https://www.linkedin.com/learning/css-layouts-from-float-to-flexbox-and-grid)

[Exercise files](https://github.com/christinatruong/css-layouts)

## Early day layouts

* **html tables**

  Usage: displaying tabular data

  row: `<tr>`, heading: `<th>`, data: `<td>`

  attr: colspan and rowspan to span data across multiple rows and cols

  pre css, con: accesibility issues

  only relevant usage to these days: html emails

## CSS layouts

* Normal flow - default layout when no css
* Floats - replaced table-based layouts
* Positioning - move elements out of normal flow, used for components within a page layout
* Flexbox - flexible new ways for aligning, 1 axis
* Grid - newest, complex layouts with rows and cols

## Normal flow

* How the browser lays out HMTL elements by default
* Same order in which elements appear in HTML
* Block level elements: stacked on top of one another
* Inline element: display side by side
* Block vs inline categorization applies up to HTML 4.0.1, HTML 5 uses more complex content categories. Still applies when it comes to CSS.
* Using CSS for layout, we move elements away from normal flow
* Box model properties

  ![Box properties](/images/box-properties-small.png)
* Display property changes display behaviours of elements in normal flow
* Box sizing
  * **content-box** (default): padding and border increase the size of element
  * **border-box**: pushes content inward to include padding and border to maintain height and width
* Float property removes elements from the normal flow
  * Changes the behaviour of the floated element AND the elements that follow it
* Clear property return elements to normal flow after an element has been floated
  * You may need to clear the flow on the next element, if it exists. If not self clear the float on parent element (clearfix hack or display: flow-root)

## 3 columns layout (nav, main, sidebar)
  * Float
    * Need to move nav before main in HTML since there's no reodering (goes against accessibility)
    * No equal column height. There are some hacks, pointless, better go with another approach
  * Position
    * **Relative** stays in the normal flow. Combine with offset props: top, left, bottom, right to fine tune
    * **Absolute** moves it out of normal flow. Positioned relative to its closest **positioned** ancestor. If none, then relative to body.
    * **Fixed**
    * **Sticky**: mixes fixed with relative to always be visible in viewport
    * **Static** (default): not positioned, normal flow
    * Stick to using position for styling small page components rather than layouts
  * Flexbox
    * One dimensional: items layed out on a single axis (columns OR rows)

      ![Flex container](/images/flex-small.png)

      Rows and columns by wrapping flex items or nesting flex containers
    * Allows us to create a responsive design without media queries
    * You can nest flex containers, so flex items become flex containers themselves
    * Container
      * **display: flex | inline-flex**
      * Two axis: main axis and cross axis
      * **flex-direction: row** makes main axis horizontal. **row-reverse** flips direction
      * **flex-direction: column** mankes main axis vertical. **column-reverse** flips direction
      * **flex-wrap: nowrap | wrap**. **wrap-reverse** reverses order in the cross axis
      * **flex-flow: shortuct for direction wrap**
      * **justify-content** align items along the main axis
    * Items
      * Flexible, equal height (determined by the largest column)
      * Sizing
        * **flex-basis** initial size "ideal sizing" (takes any css unit)
        * **flex-grow** how items expand if there is extra space (unit less: ex 1)
        * **flex-shrink** how items shrink is there is not (unit less: ex 1)
        * shorthand **flex: grow shrink basis;**
        * flex-grow determines a ratio. If flex-basis <> 0, 1 vs 2 doesn't mean double the size but how the amount of **available space** will be distributed to each item (1/3 vs 2/3). For a flex basis of 0, **all space** gets distributed
        * **order** changes order of items without changing HTML
  * Grid
    * Container
      * **display: grid | inline-grid**
      * **grid-template-colums**, **grid-template-rows** create columns and rows. Values examples:

            // 4 100px rows|columns
            100px, 100px, 100px, 100px
            // shorthand
            repeat(4, 100px)
            // 25% + 3 100px
            25%, repeat(3, 100px)
            // fr, new flexible unit, a fraction of the available space in the grid container
            repeat(4, 1fr)
            // using minmax to set range instead of fixed value
            repeat(2, minmax(100px, auto))
      * **gap** gutter between rows an columns. Combine with using **fr** units for your template, not to overflow grid container after adding gaps. Shorthand for **row-gap**, **column-gap**
    * Items
      * Placing items in the grid: **grid-column**, **grid-row**

        ![Placing grid items](/images/grid-items-positioning.png)
