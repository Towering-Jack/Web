# HTML笔记

[TOC]

---

## 常用标签

### 标题标签

1~6级标题，重要程度依次==递减==

```html
<h1>一级标题</h1>
<h2 align="center">二级标题</h2>
<h6>六级标题</h6>
```

- align属性：用于设置文字对齐方式，共有四种对齐方式
 `<!-- left center right justify -->`

### 段落标签

用于分段显示，独占一行
有**加粗、下划线、倾斜、删除**四种格式化标签可选

```html
<p>
    这是段落标签
    <b>这是加粗标签</b>
    <u>这是下划线标签</u>
    <i>这是倾斜标签</i>
    <s>这是删除线标签</s>
</p>
<p>
    这是段落标签
    <strong>这是加粗标签</strong>
    <ins>这是下划线标签</ins>
    <em>这是倾斜标签</em>
    <del>这是删除线标签</del>
</p>
```

### 换行标签和水平线标签

换行标签：`<br>`
水平线标签：`<hr size="5" color="red" align="left" width="800">`

### 媒体标签

#### 图片标签

`<img src="文件的路径" alt="替换文本，图片加载失败的时候显示。" title="提示文本，鼠标悬停的时候显示。">`

#### 音频标签

`<audio src="文件的路径" controls autoplay loop></audio><br>`

- controls属性：显示播放的控件
- autoplay属性：自动播放
- loop属性：循环播放

#### 视频标签

`<video src="文件的路径" controls autoplay muted></video>`

- muted属性：配合autoplay属性实现**自动静音播放**

#### 超链接标签

- a标签默认文字有**下划线**
- a标签从未点击过，默认文字显示**蓝色**
- a标签点击过之后，文字显示为**紫色**（清除浏览器历史记录可恢复蓝色）

`<a href="https://www.baidu.com/" title="指向链接显示的名字" target="_blank">百度一下</a>`

- href属性：
  - **#** ：回到网页顶部；
  - **#name** ：本地跳转
- target属性：
**_self** ：默认值，在当前窗口中跳转
**_blank** ：在新窗口中跳转

### 没有语义的布局标签

#### DIV标签

div是一个==块级元素==，这意味着它的内容自动地从一个新行开始

#### SPAN标签

span是一个==行内元素==，不会自动换行

### 有语义的布局标签

| 标签名      | 语义       |
| ----------- | ---------- |
| **header**  | 网页头部   |
| **nav**     | 网页导航   |
| **footer**  | 网页底部   |
| **aside**   | 网页侧边栏 |
| **section** | 网页区块   |
| **article** | 网页文章   |

### 字符实体

| 显示结果 | 描述            | 实体名称(后面要接";") |
| -------- | --------------- | --------------------- |
|          | 空格            | &nbsp                 |
| <        | 小于号          | &lt                   |
| >        | 大于号          | &gt                   |
| &        | 和号            | &amp                  |
| '        | 引号            | &quot                 |
| `        | 撇号            | &apos                 |
| ￥        | 元              | &yen                  |
| ©        | 版权(copyright) | &copy                 |

---

## 列表

### 无序列表

在网页中表示一组**无顺序**之分的列表
列表的每一项前默认显示圆点标识

```html
<ul type="circle">
    <li>榴莲</li>
    <li>香蕉</li>
</ul>
```

- type属性：
  - **circle** ：空心圆点
  - **square** ：实心方块

### 有序列表

在网页中表示一组**有顺序**之分的列表
列表的每一项前默认显示序号标识

```html
<ol type="I" start="3">
    <li>张三：100</li>
    <li>李四：90</li>
    <li>王五：80</li>
    <li>赵六：70</li>
</ol>
```

- type属性：可使用阿拉伯数字、英文字母、罗马数字
 `<!-- 1 A a I i -->`
- start属性：从数字或字母几开始

### 自定义列表

```html
<dl>
    <dt>这是自定义列表的标题</dt>
    <dd>内容1</dd> <!-- 会根据dt自动缩进 -->
    <dd>内容2</dd>
</dl>
```

---

## 表格

在网页中以**行+列**的单元格的方式整齐展示和数据

```html
<table>
    <!-- 表格标题 -->
    <caption><strong>学生成绩单</strong></caption>

    <thead>
        <tr>
            <!-- 用th代替td -->
            <th>姓名</th>
            <th>成绩</th>
            <th>评语</th>
        </tr>
    </thead>

    <tbody>
        <tr>
            <td>张三</td>
            <td rowspan="2">100</td> <!-- 合并单元格 -->
            <td>满分</td>
        </tr>
        <tr>
            <td>李四</td>
            <td>可惜了</td>
        </tr>
    </tbody>

    <tfoot>
        <tr>
            <td>总结</td>
            <td colspan="2">很棒</td>
        </tr>
    </tfoot>
</table>
```

- rowspan属性：跨行合并->**垂直**方向合并
- colspan属性：跨列合并->**水平**方向合并

**注意：** 只有同一个结构标签中的单元格才能合并，==不能跨结构标签==合并（不能跨thead、tbody、tfoot）

---

## 表单

`<form action=""></form>`

### input系列标签

type属性：

| type属性值   | 说明                       |
| ------------ | -------------------------- |
| **text**     | 文本框，用于输入单行文本   |
| **passwd**   | 密码框，用于输入密码       |
| **radio**    | 单选框，用于多选一         |
| **checkbox** | 复选框，用于多选多         |
| **file**     | 文件选择，用于之后上传文件 |
| **submit**   | 提交按钮，用于提交         |
| **reset**    | 重置按钮，用于重置         |
| **button**   | 普通按钮，默认无功能       |

#### 文本框

`<input type="text" placeholder="请输入用户名">`

- placeholder属性：占位符，提示用户输入内容的文本

#### 密码框

`<input type="password" placeholder="请输入密码">`

#### 单选框

> label 标签为 input 元素定义标签（label）。
> label 元素不会向用户呈现任何特殊的样式。不过，它为鼠标用户改善了可用性，因为如果用户点击 label 元素内的文本，则会切换到控件本身。

两种用法：

```html
<label><input type="radio" name="gender" checked>男</label>
<label><input type="radio" name="gender">女</label>
```

```html
<label for="male">Male</label>
<input type="radio" name="sex" id="male">

<label for="female">Female</label>
<input type="radio" name="sex" id="female">
```

- name属性：需要设置为相同的属性值，才能实现单选效果
- check属性：默认选中

#### 复选框

```html
<label><input type="checkbox" name="like_type" checked>可爱</label>
<label><input type="checkbox" name="like_type" checked>性感</label>
<label><input type="checkbox" name="like_type">御姐</label>
<label><input type="checkbox" name="like_type">萝莉</label>
<label><input type="checkbox" name="like_type">小鲜肉</label>
<label><input type="checkbox" name="like_type">大叔</label>
```

#### 文件选择

`<input type="file" multiple>`

- multiple：多文件选择

#### 按钮

```html
提交按钮：<input type="submit">
重置按钮：<input type="reset">

普通按钮：<input type="button">

<button>默认为普通按钮</button>
<button type="submit">提交按钮</button>
```

### select下拉菜单标签

在网页中提供多个选择项的下拉菜单表单控件

- select标签：下拉菜单的整体
- option标签：下拉菜单的每一项

```html
<select name="city">
    <option value="1">北京</option>
    <option value="2">上海</option>
    <option value="3">广州</option>
    <option value="4" selected>深圳</option>
</select>
```

- selected属性：下拉菜单的默认选中

### textarea文本域标签

在网页中提供可输入多行文本的表单控件

`<textarea name="" id="" cols="30" rows="10"></textarea>`

- cols属性：规定了文本域内可见宽度
- rows属性：规定了文本域内可见行数

**注意：** 右下角可以拖拽改变大小
