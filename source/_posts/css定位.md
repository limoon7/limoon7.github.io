---
title: CSS 定位
date: 2019-12-17 08:49:24
category: 前端
tags: css
author: lemon
---


# position

position 属性用来指定一个元素在网页上的位置，一共有5种方式，即position属性主要有五个值。

## static

1. static是position属性的默认值。如果省略position属性，浏览器就认为该元素是static定位。
2. 这时，浏览器会按照源码的顺序，决定每个元素的位置，这称为"正常的页面流"（normal flow）。每个块级元素占据自己的区块（block），元素与元素之间不产生重叠，这个位置就是元素的默认位置
3. 注意，static定位所导致的元素位置，是浏览器自主决定的，所以这时top、bottom、left、right这四个属性无效。

## relative,absolute,fixed

1. 三个属性的共同点是 ”都是相对于某个基点的定位“，不同之处在于”基点不同“

### relative

1. relative表示，相对于默认位置（即static时的位置）进行偏移，即定位基点是元素的默认位置。
2. 它必须搭配top、bottom、left、right这四个属性一起使用，用来指定偏移的方向和距离。

### absolute

1. absolute相对于上级元素（一般是父元素）进行偏移，即定位基点是父元素
2. **注意**：定位基点（一般是父元素）不能时static定位，否则定位基点就会变成整个网页的根元素html（会一直向上寻找不是static定位的父元素）。另外，absolute定位也必须搭配top、bottom、left、right这四个属性一起使用。
3. 注意，absolute定位的元素会被"正常页面流"忽略，即在"正常页面流"中，该元素所占空间为零，周边元素不受影响。

### fixed

1. fixed表示，相对于视口（viewport，浏览器窗口）进行偏移，即定位基点是浏览器窗口。这会导致元素的位置不随页面滚动而变化，好像固定在网页上一样
2. 它如果搭配top、bottom、left、right这四个属性一起使用，表示元素的初始位置是基于视口计算的，否则初始位置就是元素的默认位置。

## sticky

1. sticky跟前面四个属性值都不一样，它会产生动态效果，很像relative和fixed的结合：一些时候是relative定位（定位基点是自身默认位置），另一些时候自动变成fixed定位（定位基点是视口）。
2. 因此，它能够形成"动态固定"的效果。比如，网页的搜索工具栏，初始加载时在自己的默认位置（relative定位）。
3. sticky生效的前提是，必须搭配top、bottom、left、right这四个属性一起使用，不能省略，否则等同于relative定位，不产生"动态固定"的效果。原因是这四个属性用来定义"偏移距离"，浏览器把它当作sticky的生效门槛。
4. 它的具体规则是，当页面滚动，父元素开始脱离视口时（即部分不可见），只要与sticky元素的距离达到生效门槛，relative定位自动切换为fixed定位；等到父元素完全脱离视口时（即完全不可见），fixed定位自动切换回relative定位。

### sticky 应用

1. 堆叠效果

```css
div {
  position: sticky;
  top: 0;
}
```

2. 表格的表头锁定

```css
th {
  position: sticky;
  top: 0; 
}
```

1. 需要注意的是，sticky必须设在<th>元素上面，不能设在<thead>和<tr>元素，因为这两个元素没有relative定位，也就无法产生sticky效果