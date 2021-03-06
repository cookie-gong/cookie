---
title: 弹性盒模型
date: 2021-11-24 22:14:30
author: cookie
img: ../images/05.jpg
top: true
cover: false # 表示该文章是否需要加入到首页轮播封面中
coverImg: ../images/34.jpg # 表示该文章在首页轮播封面需要显示的图片路径，如果没有，则默认使用文章的特色图片
password: 8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92
toc: true
mathjax: false
summary: CSS 弹性盒模型
categories: CSS
tags:
  - CSS
  - flex
  - 弹性布局
---

## CSS3 弹性盒子（Flex Box）

### 弹性盒子内容

**CSS3 弹性盒（Flexible Box 或 flexbox），是一种当前页面需要适应不同的屏幕大小以及设备类型时确保元素拥有恰当的行为的布局方式。**

- 弹性盒子由弹性容器（Flex container）和弹性子元素（Flex item）组成
- 弹性容器通过设置 display 属性的值位 flex 或 inline-flex 将其定义为弹性容器。
- 弹性容器内包含了一个或多个弹性子元素。
- 弹性容器外及弹性子元素内是正常渲染的。弹性盒子只定义了弹性子元素如何在弹性容器内布局。
  弹性子元素通常在弹性盒子内一行显示。默认情况每个容器只有一行。

#### flex-direction

flex-direction 属性制定了弹性子元素在父容器中的位置。

> `flex-direction: row | row-reverse | column | column-reverse`

各个值解析:

- **row**: 横向从左到右排列（左对齐），默认的排列方式。
- **row-reverse**: 反转横向排列（右对齐，从后往前排，最后一项排在最前面。）
- **column**: 纵向排列。
- **column-reverse**: 反转纵向排列，从后往前排，最后一项排在最上面。

#### justify-content

内容对齐（justify-content）属性应用在弹性容器上，把弹性项沿着弹性容器的主轴线对齐。

> `justify-content: flex-start | flex-end | center | space-between | space-around`

各个值解析:

- **flex-start**：
  弹性项目向行头紧挨着填充。这个是默认值。
- **flex-end**：
  弹性项目向行尾紧挨着填充。
- **center**：
  弹性项目居中紧挨着填充。（如果剩余的自由空间是负的，则弹性项目将在两个方向上同时溢出）。
- **space-between**：
  弹性项目平均分布在改行上。如果剩余空间为负或者只有一个弹性项，则该值等同于 flex-start。否则，第一个弹性项的外边距和行的主轴线边线对齐，而最后一个弹性项的外边距和行的 main-end 边线对齐，然后剩余的弹性项分布在该行上，相邻项目的间隔相等。
- **space-around**：
  弹性项目平均分布在该行上，两边留着一半的间隔空间。如果剩余空间为负或者只有一个弹性项，则该值等同于 center。否则，弹性项目沿该行分布，且彼此间隔相等，同时首尾两边和弹性容器之间留有一半的间隔。

#### align-items

align-items 设置或检索弹性盒子元素在侧轴（纵轴）方向上的对齐方式。

> `align-items: flex-start | flex-end | center | baseline | stretch`

各个值解析:

- **flex-start**：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
- **flex-end**：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
- **center**：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
- **baseline**：如弹性盒子元素的行内轴和侧轴为同一条，则该值与 flex-start 等效。其他情况下，该值将参与基线对齐。
- **stretch** `默认值`：如果指定侧轴大小的属性值为 auto，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵循 min/max-width/height 属性的限制。

#### flex-wrap

**flex-wrap** 属性用于指定弹性盒子的子元素换行方式。

> `flex-wrap: nowrap | wrap | wrap-reverse | initial | inherit`

各个值解析:

- **nowrap** 默认，弹性容器为当行。该情况下弹性子项可能会溢出容器。
- **wrap** 弹性容器为多行。该情况下弹性子项溢出的部分会放置到新行，子项内部会发生断行。
- **wrap-reverse** 反转 wrap 排列。默认是从上往下排列的，而这是从下往上换行。

#### align-content

**align-content** 属性用于修改 flex-wrap 属性的行为。类似于 align-items，但它不是设置弹性子元素的对齐，而是设置各个行的对齐。

> align-content: flex-start | flex-end | center | space-between | space-around | stretch

各个值解析:

- stretch：默认，各行将会伸展以占用剩余的空间。
- flex-start：各行向弹性盒容器的起始位置堆叠。
- flex-end：各行向弹性盒容器的结束位置堆叠。
- center：各行向弹性盒容器的中间位置堆叠。
- space-between：各行在弹性盒容器中平均分布。
- space-around：各行在弹性和容器中平均分布，两端保留子元素与子元素之间间距大小的一半。

### 弹性子元素属性

#### order 排序

- `integer`: 用整数值来定义排序顺序，数值小的排在前面。可以为负值。就是通过在子元素中设置 order 属性改变 DOM 元素排列顺序。

#### margin 对齐

- 设置 margin 值为 auto，自动获取弹性容器中剩余的空间。所以设置垂直方向 margin 值为 auto，可以使弹性子元素在弹性容器的两上轴方向都完全居中。

以下实例中子元素布局位于父元素中央位置：

```CSS
.father {
    display:flex;
    width:200px;
    height:200px;
}

.son {
    width: 100px;
    height: 100px;
    margin: auto;
}
```

#### align-self

**align-slef** 属性用于设置弹性元素自身在侧轴（纵轴）方向上的对齐方式。

> `align-self: auto | flex-start | flex-end | center | baseline | stretch`

各个值解析:

- `auto`：如果 align-self 的值为 auto，则其计算值为元素的父元素的 align-items 值，如果其没有父元素，则计算值为 stretch。
- `flex-start`：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴起始边界。
- `flex-end`：弹性盒子元素的侧轴（纵轴）起始位置的边界紧靠住该行的侧轴结束边界。
- `center`：弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。
- `baseline`：如弹性盒子元素的行内轴与侧轴为同一条，则该值与 flex-start 等效。其它情况下，该值将参与基线对齐。
- `stretch`：如果指定侧轴大小的属性值为 auto，则其值会使项目的边距盒的尺寸尽可能接近所在行的尺寸，但同时会遵照 min/max-width/height 属性的限制。

#### flex

`flex` 属性用于指定弹性子元素如何分配空间。

### 语法

> `flex: auto | initial | none | inherit | [ flex-grow ] || [ flex-shrink ] || [ flex-basis ]`

各个值解析:

- auto: 计算值为 1 1 auto
- initial: 计算值为 0 1 auto
- none：计算值为 0 0 auto
- inherit：从父元素继承
- [flex-grow]：定义弹性盒子元素的扩展比率。
- [flex-shrink]：定义弹性盒子元素的收缩比率。
- [flex-basis]：定义弹性盒子元素的默认基准值。
