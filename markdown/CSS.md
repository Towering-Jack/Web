# CSS笔记

[TOC]

---

## 选择器

### 标签选择器

结构： 标签名 { css属性名:属性值; }

```css
p {
    color: red;
    background-color: whitesmoke;
    ...
}
```

### 类选择器

结构： .类名 { css属性名：属性值; }

```css
.box {
    color: red;
    background-color: whitesmoke;
    ...
}
```

### id选择器

结构： #id属性值 { css属性名：属性值; }

```css
#gender {
    color: red;
    background-color: whitesmoke;
    ...
}
```

> class类名与id属性值的区别
>
> - class类名相当于姓名，可以重复，一个标签可以同时有多个class类名
> - id属性值相当于身份证号码，不可重复，一个标签只能有一个id属性值
>   - id一般配合js使用，除非特殊情况，否则不要使用id设置样式

### 通配符选择器

结构： * { css属性名：属性值; }

```css
* {
    margin: 0;
    padding: 0;

    /* 内减模式 */
    box-sizing: border-box;
}
```

### 选择器优先级

- 特性：不同选择器具有不同的优先级，优先级高的选择器样式会覆盖优先级低选择器样式
- 优先级公式：
  - 继承 < 通配符选择器 < 标签选择器 < 类选择器 < id选择器 < 行内样式 < !important

> **关于!important**
>
> ```css
> p{
>     color: red !important;
> }
> ```
>
> 1. !important写在属性值的后面，分号的前面
> 2. !important不能提升继承的优先级，只要是继承优先级最低

---

## 复合选择器

### 后代选择器

选择器语法： 选择器1 选择器2 { css }

```css
div p {
    font: 24px/1.5 微软雅黑;
    color: aqua;
    ...
}
```

### 子代选择器

选择器语法： 选择器1 > 选择器2 { css }

```css
div > p {
    font: 24px/1.5 微软雅黑;
    color: aqua;
    ...
}
```

### 并集选择器

作用：同时选择多组标签，设置相同的样式
选择器语法： 选择器1 , 选择器2 { css }

```css
div , p {
    font: 24px/1.5 微软雅黑;
    color: aqua;
    ...
}
```

### 交集选择器

作用：选中页面中**同时满足**多个选择器的标签
选择器语法： 选择器1选择器2 { css }

```css
div.box {
    font: 24px/1.5 微软雅黑;
    color: aqua;
    ...
}
```

> 交集选择器中的选择器之间是==紧挨==着的，没有东西分隔
> 交集选择器中如果有**标签选择器**，标签选择器必须写在最前面

### 伪类选择器

#### hover伪类选择器

作用：选中鼠标悬停在元素上的状态，设置样式
选择器语法：选择器:hover { css }

```css
p:hover {
    color: red;
    text-decoration: underline;
}
```

#### 结构伪类选择器

- 场景：常用于查找某父级选择器中的子元素
- 作用：根据元素在HTML中的结构关系查找元素

##### nth-child系列

| 选择器(n为自然数)      | 说明                                     |
| ---------------------- | ---------------------------------------- |
| E:first-child {}       | 匹配父元素中第一个子元素，并且是E元素    |
| E:last-child {}        | 匹配父元素中最后一个子元素，并且是E元素  |
| E:nth-child(n) {}      | 匹配父元素中第n个子元素，并且是E元素     |
| E:nth-last-child(n) {} | 匹配父元素中倒数第n个子元素，并且是E元素 |

```css
li:first-child {
    color: skyblue;
}

li:nth-child(-n+5) {
    color: skyblue;
}

li:nth-last-child(2) {
    color: skyblue;
}
```

##### nth-of-type系列

| 选择器(n为自然数)   | 说明                                         |
| ------------------- | -------------------------------------------- |
| E:nth-of-type(n) {} | 只在父元素的同类型(E)子元素范围中，匹配第n个 |

```css
a:nth-of-type(1) {
    color: skyblue;
}
```

> 区别：
>
> - :nth-child → 直接在所有孩子中数个数
> - :nth-of-type → 先通过该**类型**找到符合的一堆子元素，然后在这一堆子元素中数个数

### 伪元素选择器

一般页面中的非主体内容可以使用伪元素，由**CSS**模拟出的标签效果

```css
E::before {
    content: "老鼠";
}

E::after {
    content: "大米";
}
```

- 必须设置content属性才能生效
- 伪元素默认是行内元素

### 选择器权重计算

如果是复合选择器，此时需要通过权重叠加计算方法，判断最终哪个选择器优先级最高会生效

1. 先判断选择器是否能直接选中标签，如果不能直接选中 → 是继承，优先级最低 → 直接pass
2. 通过**权重计算公式**，判断谁权重最高

```css
/* (行内, id, 类, 标签) */

/* (0, 2, 0, 0) */
#father #son {
    color: blue;
}

/* (0, 1, 1, 1) */
#father p.c2 {
    color: black;
}

/* (0, 0, 2, 2) */
div.c1 p.c2 {
    color: red;
}

/* 继承, 最低 */
#father {
    color: green !important;
}

/* 继承, 最低 */
div#father.c1 {
    color: yellow;
}
```

```html
<div id="father" class="c1">
    <p id="son" class="c2">
        这行文本是蓝色的。
    </p>
</div>
```

---

## 样式

### 字体样式

```css
.font {
    /* 格式：font: style weight size/line-height family */
    /* 先写复合属性，style和weight可以省略 */
    font: italic 700 32px/2 宋体;

    /* 无衬线字体sans-serif */
    font-family: 微软雅黑, 宋体, sans-serif;
    
    /* 首行缩进两个字符 */
    text-indent: 2em;

    /* 字符间距 */
    letter-spacing: 2px;

    /* 文字对齐方式: left center right justify */
    text-align: center;

    /* underline下划线, line-througt删除线, overline上划线, none无装饰线 */
    text-decoration: underline;
}
```

> 颜色取值：关键字、 rgb表示法、 rgba表示法、十六进制...

- font-weight属性：
  - 100 ~ 900的整百数
    - 400: normal
    - 700: bold
- font-family属性：
  - 无衬线字体（sans-serif）
  - 衬线字体（serif）
  - 等宽字体（monospace）

> - 无衬线字体（sans-serif）
>   1. 特点：文字笔画粗细均匀，并且首尾无装饰
>   2. 场景：网页中大多采用无衬线字体
>   3. 常见该系列字体：黑体、 Arial
> - 衬线字体（serif）
>   1. 特点：文字笔画粗细不均，并且首尾有笔锋装饰
>   2. 场景：报刊书籍中应用广泛
>   3. 常见该系列字体：宋体、 Times New Roman
> - 等宽字体（monospace）
>   1. 特点：每个字母或文字的宽度相等
>   2. 场景：一般用于程序代码编写，有利于代码的阅读和编写
>   3. 常见该系列字体： Consolas、 fira code

### 背景样式

```css
.bg {
    width: 600px;
    height: 400px;

    /* background连写： color image repeat position */
    background: antiquewhite url('图片路径') no-repeat 300px 100px;

    background-color: pink;
    background-image: url('图片路径');
    background-repeat: repeat-y;
    background-position: center center;
}
```

- background-repeat属性：背景平铺设置
  - **repeat** ：默认值，水平和垂直方向都平铺
  - **no-repeat** ：不平铺
  - **repeat-x** ：沿着水平方向(x轴)平铺
  - **repeat-y** ：沿着垂直方向(y轴)平铺

#### 背景渐变

```css
background-image: linear-gradient(
    transparent,
    rgba(0, 0, 0, .5)
);
```

- **transparent** ：纯透明黑色 rgba(0, 0, 0, 0)

---

## 元素显示模式

### 块级元素

`display: block`

- 显示特点：
  1. 独占一行（一行只能显示一个）
  2. 宽度默认是父元素的宽度，高度默认由内容撑开
  3. 可以设置宽高
- 代表标签：
  - div、 p、 h系列、 ul、 li、 dl、 dt、 dd、 form、 header、 nav、 footer...

### 行内元素

`display: inline`

- 显示特点：
  1. 一行可以显示多个
  2. 宽度和高度默认由内容撑开
  3. 不可以设置宽高
- 代表标签：
  - a、 span、 b、 u、 i、 s、 strong、 ins、 em、 del...

### 行内块元素

`display: inline-block`

- 显示特点：
  1. 一行可以显示多个
  2. 可以设置宽高
- 代表标签：
  - input、 textarea、 button、 select...

---

## 盒子模型

CSS 中规定每个盒子分别由： **内容区域（content）**、**内边距区域（padding）**、**边框区域（border）**、**外边距区域（margin）** 构成

### 内容区域（content）

```css
width: 800px;
height: 400px;
background-color: pink;
```

### 边框区域（border）

```css
/* 格式：border: width style color */
border: 10px solid red;

/* 单方向设置：top bottom left right */
border-bottom: 5px dashed blue;
```

- border-style属性：
  - **solid** ：实线
  - **dashed** ：虚线
  - **dotted** ：点线

### 内边距区域（padding）

```css
padding: 10px 15px 20px 25px;
padding: 10px 15px 20px;
padding: 10px 15px;
padding: 10px;
```

- 4个值：上 / 右 / 下 / 左（顺时针）
- 3个值：上 / 左右 / 下
- 2个值：上下 / 左右
- 1个值：上下左右

### 外边距区域（margin）

```css
/* 版心居中，左右自适应用auto */
margin: 20px auto;
```

### 补充

#### 清除默认内外边距

> - 浏览器会默认给部分标签设置默认的margin和padding，但一般在项目开始前需要先清除这些标签默认的margin和padding，后续自己设置
> - 可以使用通配符选择器进行清除

#### 外边距折叠现象

- 合并现象
  - 场景：**垂直布局**的**块级元素**，上下的 margin 会合并，最终两者距离为两者 margin 的最大值
  - 解决办法：只给其中一个盒子设置 margin 即可
- 塌陷现象
  - 场景：**互相嵌套**的**块级元素**，子元素的 ==margin-top== 会作用在父元素上，导致父元素一起往下移动
  - 解决办法：
    1. 给父元素设置 border-top 或者 padding-top （分隔父子元素的margin-top）
    2. 给父元素设置 `overflow： hidden`
    3. 转换成行内块元素
    4. 设置浮动

---

## 浮动

- 浮动的框可以向左或向右移动，直到它的外边缘碰到包含框或另一个浮动框的边框为止
- 由于浮动框不在文档的普通流中，所以文档的普通流中的块框表现得就像浮动框不存在一样

```css
.left {
    float: left;

    width: 300px;
    height: 300px;
}

.right {
    float: right;

    width: 300px;
    height: 300px;
}
```

### 清除浮动

- 如果子元素浮动了，此时子元素不能撑开标准流的块级父元素
- 子元素浮动后脱标，不占位置
- 清除浮动的方法：
  1. 直接设置父元素高度
  2. 额外标签法
     1. 在父元素内容的最后添加一个块级元素
     2. 给添加的块级元素设置 clear:both
  3. 单伪元素清除法
     - 用伪元素替代了额外标签
  4. ==双伪元素清除法==
  5. 给父元素设置 `overflow : hidden`

```css
/* 双伪元素清除法：解决外边距塌陷 */
.clearfix3::before,
.clearfix3::after {
    content: '';
    display: table;
}
.clearfix3::after {
    clear: both;
}
```

---

## 定位

定位之后的元素层级最高，可以层叠在其他盒子上面

- position设置定位的方式：

| 定位方式 | 属性值   |
| -------- | -------- |
| 静态定位 | static   |
| 相对定位 | relative |
| 绝对定位 | absolute |
| 固定定位 | fixed    |

- 设置偏移值：水平+垂直就近取一个即可

### 静态定位

- 静态定位是默认值，就是之前认识的标准流。
- 不能通过方位属性进行移动

### 相对定位

- 需要配合方位属性实现移动
- 相对于自己原来位置进行移动
- 在页面中占位置，没有脱标

```css
position: relative;
left: 100px;
top: 100px;
```

### 绝对定位

- 需要配合方位属性实现移动
- 相对于最近的**非静态定位**的**祖先元素**进行定位移动
- 祖先元素中没有定位，则默认相对于浏览器进行移动
- 在页面中不占位置，已经脱标

```css
position: absolute;
left: 100px;
top: 100px;
```

> 配合绝对定位（子绝父相）
> 让子元素相对于父元素进行自由移动

### 固定定位

- 需要配合方位属性实现移动
- 相对于浏览器进行定位移动
- 在页面中不占位置，已经脱标

```css
position: fixed;
left: 100px;
top: 100px;
```

### 层级关系

- 标准流 < 浮动 < 定位
- 相对、绝对、固定默认层级相同，此时HTML中写在下面的元素层级更高，会覆盖上面的元素
- 通过**z-index**属性修改定位元素的层级
  - 取整数，默认是0。取值越大，显示顺序越靠上

---

## 平面转换

改变盒子在平面内的形态（位移、旋转、缩放）

### 位移

`transform: translate(水平移动距离, 垂直移动距离);`

- translate()如果只给出一个值, 表示x轴方向移动距离
- 单独设置某个方向的移动距离：**translateX()** 或 **translateY()**
- 取值：可用 **像素单位** 或者 **百分比**(基于盒子自身尺寸)

**注意** ：X轴正向为右，Y轴正向为==下==

#### 移动到父级盒子中间

```css
left: 50%;
top: 50%;

transform: translate(-50%, -50%);
```

#### 双开门效果

```css
.box {
    width: 1000px;
    height: 600px;
    margin: 0 auto;
    background: url('背景图片路径');

    /* 溢出隐藏 */
    overflow: hidden;
}

.box::before,
.box::after {
    float: left;
    content: '';
    width: 50%;
    height: 600px;
    background-image: url('显示图片路径');

    /* 持续时间 */
    transition: all 0.5s;
}

/* 右半部分显示图片 */
.box::after {
    /* right也可换成 100% */
    background-position: right 0;
}

/* 鼠标移入的时候的位置改变的效果 */
.box:hover::before {
    transform: translate(-100%);
}

.box:hover::after {
    transform: translateX(100%);
}
```

### 旋转

`transform: rotate(角度);`

- 角度单位是deg
- 取值为正，则顺时针旋转，反之为逆时针旋转

`transform-origin: 原点水平位置 原点垂直位置;`

- transform-origin属性：改变转换原点
- 默认圆点是盒子中心点
- 取值：
  - 方位名词（left、top、right、bottom、center）
  - 像素单位数值
  - 百分比（参照盒子自身尺寸计算）

### 缩放

`transform: scale(x轴缩放倍数, y轴缩放倍数);`

- 一般情况下，只为scale设置一个值，表示x轴和y轴等比例缩放
- scale值大于1表示放大，scale值小于1表示缩小

### transform复合属性

```css
transform:  translate(<translation-value>[,<translation-value>]?)
            rotate(<angle>)
            scale(<number>[,<number>]?)
            skew(<angle>[,<angle>]?);
```

- **旋转**会改变网页元素的坐标轴向
- 先写旋转，则后面的转换效果的轴向**以旋转后的轴向为准**，会影响转换结果

---

## 补充功能

### iconfont字体图标

[iconfont素材下载](https://www.iconfont.cn/)

> 在iconfont图标库中，找到需求的图标
> 先清空自己当前的购物车，避免污染，然后按F12进入console控制台
> 在控制台中，复制以下代码
>
> ```js
> 第一种方法
> var iconFontList = document.querySelectorAll('.icon-gouwuche1')
> Array.from(iconFontList).forEach(v => v.click())
>
> 第二种方法
> var iconFontList = document.querySelectorAll('.icon-gouwuche1');
> 
> for(var i = 0; i < iconList.length; i++) {
>     iconFontList[i].click();
> }
> ```
>
> 稍微等几秒钟，图标购物车就有当前所有的图标了
> 在购物车中，加入到图标项目，然后去我的项目中下载
