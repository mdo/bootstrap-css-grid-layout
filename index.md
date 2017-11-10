---
layout: default
---

# Bootstrap's grid in CSS Grid
This demo explores how we might take as much of the complex responsive [grid system from Bootstrap 4](https://getbootstrap.com/docs/4.0/layout/grid/) and rebuild it with only CSS Grid. No Sass, no flexbox, no floats. Ideally we end up with all the same functionality, but probably just less browser support.

Browser support currently includes IE11, Edge 15+, latest Chrome (desktop and Android), latest Safari (mobile and desktop), latest Firefox. Flexbox, by contrast, is supported across those browsers in earlier versions—IE10+, Edge 12+, Android 4.4, etc. For more details, see <https://caniuse.com/#feat=css-grid> and <https://caniuse.com/#feat=flexbox>.

This document doesn't cover every part of CSS Grid Layout, just what we need to recreate as much of Bootstrap's existing flexbox grid implementation.

---

## Defining our grid

- The grid is 12 columns with a 30px gutter.
- We have five breakpoints in our responsive grid: extra small (no [infix](https://en.wikipedia.org/wiki/Infix)), small (`sm`), medium (`md`), large (`lg`), and extra large (`xl`).
- Due to limitations with CSS Grid, we need additional responsive `.row-*` classes. These are not present in Bootstrap's grid.
- We're using Jekyll to compile this page and render from Markdown. We have a single layout, a custom `highlight` plugin, and three CSS files (docs layout and type, code syntax, and the grid itself).

---

## About CSS Grid Layout
CSS Grid Layout—not to be confused with a CSS grid—introduces new properties, values, and units. Here's a primer for those new like me.

- `display: grid` initializes the new layout module by establishing a _grid container_. Once a grid container is created, immediate children elements become _grid items_.
- Two new properties, `grid-template-columns` and `grid-template-rows`, allow you to create grid layouts in either direction on the same container. By comparison, flexbox controls layout in one of two directions, `row` or `column`.
- Another new property, `grid-gap`, lets you specify the space between each grid item. **This applies vertically and horizontally.**
- In addition to the units you've grown accustomed to using for grids (`px`, `%`, `em`, or `rem`), you can now use `fr` (short for fractional units).

---

## 12 columns
Bootstrap's grid system is based on a 12 column grid. From there, you can span multiple columns—by breakpoint—as needed. It's rare you'll have this exact setup, but it demonstrates the grid's foundation.

{% example html %}
<div class="row">
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
</div>
{% endexample %}

None of these columns have a number specified, but you can choose to specify some and let the grid do the rest. Here we've turned the first four `.col`s into `.col-4`.

{% example html %}
<div class="row">
  <div class="col-4">col-4</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
  <div>col</div>
</div>
{% endexample %}

Lastly, you can specify a number of grid columns to span for every column.

{% example html %}
<div class="row">
  <div class="col-6">col-6</div>
  <div class="col-3">col-3</div>
  <div class="col-3">col-3</div>
</div>
{% endexample %}

---

## Responsive
When we say "responsive grid", we mean controlling the behavior (vertically stack them or horizontally fill a row) and changing the number of grid columns to span by breakpoint.

### Stacked xs, columns sm+
Starts out stacked on mobile (xs), but at `sm` and up, let the horizontal columns kick in.

{% example html %}
<div class="row">
  <div class="col-sm-6">col-sm-6</div>
  <div class="col-sm-3">col-sm-3</div>
  <div class="col-sm-3">col-sm-3</div>
</div>
{% endexample %}

{% example html %}
<div class="row-sm">
  <div class="col-sm-6">col-sm-6</div>
  <div class="col-sm-3">col-sm-3</div>
  <div class="col-sm-3">col-sm-3</div>
</div>
{% endexample %}

### Stacked xs w/ mixed columns at sm and md
Starts out stacked on mobile (xs), defining particular column widths at `sm`, and then overriding those with `md` columns that apply for `md`, `lg`, and `xl`.

{% example html %}
<div class="row">
  <div class="col-sm-6 col-md-4">col-sm-6 col-md-4</div>
  <div class="col-sm-3 col-md-4">col-sm-3 col-md-4</div>
  <div class="col-sm-3 col-md-4">col-sm-3 col-md-4</div>
</div>
{% endexample %}

---

## Questions
- Does CSS Grid have an option for a column to fill available space?
- Padding on cells vs gutter (margin)? Otherwise benefit is no negative margins...
