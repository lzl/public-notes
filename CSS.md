## What is CSS selector specificity and how does it work?

浏览器通过优先级规则，判断元素展示哪些样式。优先级通过 4 个维度指标确定，我们假定以 a、b、c、d 命名，分别代表以下含义：

- a 表示是否使用内联样式 inline style. 如果使用，a 为 1，否则为 0。`<h1 style=“color: #fff;”>`
- b 表示 ID 选择器的数量。`#id`
- c 表示类选择器、属性选择器和伪类选择器数量之和。`.classes, [attributes], :hover, :focus`
- d 表示标签（类型）选择器和伪元素选择器之和。`div, p, :before, :after`

a,b,c,d 权重从左到右，依次减小。比如 0,1,0,0 的优先级高于 0,0,10,10。

- https://www.smashingmagazine.com/2007/07/css-specificity-things-you-should-know/

## Describe floats and how they work.

浮动 float 是 CSS 定位属性。浮动元素从网页的正常流动中移出，但是保持了部分的流动性，会影响其他元素的定位（比如文字会围绕着浮动元素）。这一点与绝对定位不同，绝对定位的元素完全从文档流中脱离。

如果父元素只包含浮动元素，那么该父元素的高度将塌缩为 0。我们可以通过清除 clear 从浮动元素后到父元素关闭前之间的浮动来修复这个问题。

```css
.clearfix:after {
  content: ".";
  visibility: hidden;
  display: block;
  height: 0;
  clear: both;
}
```

或者，把父元素属性设置为 `overflow: auto` 或 `overflow: hidden`，会使其内部的子元素形成块格式化上下文 Block Formatting Context，并且父元素会扩张自己，使其能够包围它的子元素。

- https://css-tricks.com/all-about-floats/

## Describe z-index and how stacking context is formed.

z-index 只能影响 position 值不是 static 的元素。

When the z-index and position properties aren’t involved, the rules are pretty simple: basically, the stacking order is the same as the order of appearance in the HTML.

When you introduce the position property into the mix, any positioned elements (and their children) are displayed in front of any non-positioned elements.

Finally, when z-index is involved, things get a little trickier. At first it’s natural to assume elements with higher z-index values are in front of elements with lower z-index values, and any element with a z-index is in front of any element without a z-index, but it’s not that simple. First of all, z-index only works on positioned elements. If you try to set a z-index on an element with no position specified, it will do nothing. Secondly, z-index values can create stacking contexts, and now suddenly what seemed simple just got a lot more complicated.

New stacking contexts can be formed on an element in one of three ways: When an element is the root element of a document (the <html> element). When an element has a position value other than static and a z-index value other than auto. When an element has an opacity value less than 1. [More rules](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context#The_stacking_context).

- https://philipwalton.com/articles/what-no-one-told-you-about-z-index/

## Describe Block Formatting Context (BFC) and how it works.

满足以下任意一条，会创建块格式化上下文：

- float 的值不是 none.
- position 的值不是 static 或 relative.
- display 的值是 table-cell、table-caption、inline-block、flex、或 inline-flex。
- overflow 的值不是 visible。
- [more rules](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Block_formatting_context)

Use cases:

- Make float content and alongside content the same height.
- Margin collapsing.

- https://www.smashingmagazine.com/2017/12/understanding-css-layout-block-formatting-context/

## What does \* { box-sizing: border-box; } do? What are its advantages?

By default, elements have `box-sizing: content-box` applied, and only the content size is being accounted for.

`box-sizing: border-box` changes how the width and height of elements are being calculated, border and padding are also being included in the calculation.

The height of an element is now calculated by the content's height + vertical padding + vertical border width.

The width of an element is now calculated by the content's width + horizontal padding + horizontal border width.

Taking into account paddings and borders as part of our box model resonates better with how designers actually imagine content in grids.

## Have you played around with the new CSS Flexbox or Grid specs?

Yes. Flexbox is mainly meant for 1-dimensional layouts while Grid is meant for 2-dimensional layouts.

- https://learncssgrid.com/
- https://cssgrid.io/
- https://gridbyexample.com/examples/
