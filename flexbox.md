# Flexbox

Main problem is how to center, align items within a container even when the size is dynamic.
Flexbox to the rescue!

## Old problem (without flexbox)
Div are displayed as block (vertically), to display them inline, you can either:
- use `display: inline-block`
- or add to `float: left`

For a given html:
```html
    <div class="main">
      <div class="container">
        <div class="box one"></div>
        <div class="box two"></div>
        <div class="box three"></div>
      </div>
      <div>Next div should go beneath</div>
    </div>
```
your CSS looks like:
```css
.container {
  width: 100%;
  background-color: white;
}

.box {
  height: 10em;
  width: 10em;
  float: left;
}
```

> Problem: 😱 😨 😰 : `Next div should go beneath` text is displayed inline. We need to "clear" using the [clearfix hacks](https://css-tricks.com/snippets/css/clear-fix/)

```css
.container:after {
  content: "";
  display: table;
  clear: both;
}
``` 
## step1: flexbox to inline 3 boxes
Add `display: flex`:

## step2: boxes to grow to take all space
```css
.box {
  height: 10em;
  width: 10em;
  flex-grow: 1;
}
```
No need to do the math and add 33.3% 🤓 

## step3: boxes to grow to take all space
If we want a different growth for each boxes, add `flex-grow: 2;` to .box 
Note the growth value is a ratio, it can be any value.

## step4: flex wrapper
If we add a min-width to our box. Reducing the size of the window, we don't want to scroll but have the dic wrap to the next column.
By adding `flex-wrap: wrap;` without media queries you get a responsive behaviour  😜 😝
```css
.container {
  display: flex;
  width: 100%;
  background-color: white;
  flex-wrap: wrap;
}

.box {
  height: 100px;
  width: 300px;
  min-width: 200px;
  flex-grow: 1;
}
```

> Note: use `flex-basis` instead of `min-width` so no scroll bar. there is a shorthabd notation: `flex: grow shrink basis`