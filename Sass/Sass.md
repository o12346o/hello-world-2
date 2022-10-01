# 1、Sass 介绍

Sass 是一个 CSS 预处理器。

Sass 是 CSS 扩展语言，可以帮助我们减少 CSS 重复的代码，节省开发时间。

Sass 完全兼容所有版本的 CSS。

Sass 扩展了 CSS3，增加了规则、变量、混入、选择器、继承、内置函数等等特性。

Sass 生成良好格式化的 CSS 代码，易于组织和维护。

Sass 文件后缀为 .scss。

## 1.1 为什么使用 Sass?

CSS 本身语法不够强大，导致重复编写一些代码，无法实现复用，而且在代码也不方便维护。

Sass 引入合理的样式复用机制，增加了规则、变量、混入、选择器、继承、内置函数等等特性。

## 1.2 Sass 是如何工作的？

浏览器并不支持 Sass 代码。因此，你需要使用一个 Sass 预处理器将 Sass 代码转换为 CSS 代码。

# 2、Sass 安装

```powershell
npm install -g sass
```

## 2.1 使用介绍

创建一个 test.scss 文件，内容为：

```scss
/* 定义变量与值 */
$bgcolor: lightblue;
$textcolor: darkblue;
$fontsize: 18px;

/* 使用变量 */
body {
  background-color: $bgcolor;
  color: $textcolor;
  font-size: $fontsize;
}
```

然后在命令行输入下面命令,

```powershell
sass test.scss 
```

即将 .scss 文件转化的 css 代码打印出来：

```powershell
@charset "UTF-8";
/* 定义变量与值 */
/* 使用变量 */
body {
  background-color: lightblue;
  color: darkblue;
  font-size: 18px;
}
```

---

我们也可以在后面再跟一个 .css 文件名，将代码保存到文件中,

```powershell
sass test.scss test.css
```

会在当前目录下生成 test.css 文件，代码如下：

```css
@charset "UTF-8";
/* 定义变量与值 */
/* 使用变量 */
body {
  background-color: lightblue;
  color: darkblue;
  font-size: 18px;
}

/*# sourceMappingURL=test.css.map */
```

# 3、Sass 变量

变量用于存储一些信息，它可以重复使用。

Sass 变量可以存储以下信息：

- 字符串
- 数字
- 颜色值
- 布尔值
- 列表
- null 值

## 3.1 Sass 变量使用 $ 符号。

以下实例设置了四个变量：myFont, myColor, myFontSize, 和 myWidth。

变量声明后我们就可以在代码中使用它：

```scss
$myFont: Helvetica, sans-serif;
$myColor: red;
$myFontSize: 18px;
$myWidth: 680px;

body {
  font-family: $myFont;
  font-size: $myFontSize;
  color: $myColor;
}

#container {
  width: $myWidth;
}
```

转换为 CSS 代码：

```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}

#container {
  width: 680px;
}
```

## 3.2 Sass 作用域

Sass 变量的作用域只能在当前的层级上有效果，

```scss
$myColor: red;

h1 {
  $myColor: green;   // 只在 h1 里头有用，局部作用域
  color: $myColor;
}

p {
  color: $myColor;
}
```

转换为 CSS 代码：

```css
body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}

#container {
  width: 680px;
}
```

---

当然 Sass 中我们可以使用 !global 关键词来设置变量是全局的，

```scss
$myColor: red;

h1 {
  $myColor: green !global;  // 全局作用域
  color: $myColor;
}

p {
  color: $myColor;
}
```

转换为 CSS 代码：

```css
h1 {
  color: green;
}

p {
  color: green;
}
```

# 4、Sass 嵌套规则与属性

## 4.1 Sass 嵌套规则

Sass 嵌套 CSS 选择器类似于 HTML 的嵌套规则：

```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  li {
    display: inline-block;
  }
  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}
```

转换为 CSS 代码：

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}
nav li {
  display: inline-block;
}
nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

## 4.2 Sass 嵌套属性

很多 CSS 属性都有同样的前缀，例如：font-family, font-size 和 font-weight ， text-align, text-transform 和 text-overflow。

在 Sass 中，我们可以使用嵌套属性来编写它们：

```scss
p {
  font: {
    family: Helvetica, sans-serif;
    size: 18px;
    weight: bold;
  }

  text: {
    align: center;
    transform: lowercase;
    overflow: hidden;
  }
}
```

转换为 CSS 代码：

```css
p {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  font-weight: bold;
  text-align: center;
  text-transform: lowercase;
  text-overflow: hidden;
}
```

# 5、Sass @import 与 Partial

## 5.1 Sass @import

Sass 可以帮助我们减少 CSS 重复的代码，节省开发时间。

我们可以安装不同的属性来创建一些代码文件，如：变量定义的文件、颜色相关的文件、字体相关的文件等。

**Sass 导入文件**

类似 CSS，Sass 支持 @import 指令。

@import 指令可以让我们导入其他文件等内容。

CSS @import 指令在每次调用时，都会创建一个额外的 HTTP 请求。但，Sass @import 指令将文件包含在 CSS 中，不需要额外的 HTTP 请求。 

【举例】创建一个 reset.scss 文件，

```scss
html,
body,
ul,
ol {
  margin: 0;
  padding: 0;
}
```

在 standard.scss文件中使用 @import 导入reset.scss 文件，

```scss
@import "reset";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

转换为 CSS 代码：

```css
html, body, ul, ol {
  margin: 0;
  padding: 0;
}

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: red;
}
```

## 5.2 Sass Partials

如果你不希望将一个 Sass 的代码文件编译到一个 CSS 文件，你可以在文件名的开头添加一个下划线。这将告诉 Sass 不要将其编译到 CSS 文件。

但是，在导入语句中我们不需要添加下划线。

【举例】建一个 _colors.scss 的文件，但是不会编译成 _colors.css 文件：

```scss
$myPink: #EE82EE;
$myBlue: #4169E1;
$myGreen: #8FBC8F;
```

如果要导入该文件，则不需要使用下划线：

```scss
@import "colors";

body {
  font-family: Helvetica, sans-serif;
  font-size: 18px;
  color: $myBlue;
}
```

# 6、Sass @mixin 与 @include

@mixin 指令允许我们定义一个可以在整个样式表中重复使用的样式。

@include 指令可以将混入（mixin）引入到文档中。

## 6.1 定义一个混入

混入(mixin)通过 @mixin 指令来定义。

```scss
@mixin important-text {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
}
```

## 6.2 使用混入

@include 指令可用于包含一混入:

```scss
.danger {
  @include important-text;
  background-color: green;
}
```

代码转换为 CSS 代码：

```css
.danger {
  color: red;
  font-size: 25px;
  font-weight: bold;
  border: 1px solid blue;
  background-color: green;
}
```

---

混入中也可以包含混入:

```scss
@mixin special-text {
  @include important-text;
  @include link;
  @include special-border;
}
```

## 6.3 向混入传递变量

混入可以接收参数。

我们可以向混入传递变量。

```scss
/* 定义混入 */
/* 混入接收两个参数 */
@mixin bordered($color, $width) {
  border: $width solid $color;
}

.myArticle {
  @include bordered(blue, 1px);  // 调用混入，并传递两个参数
}

.myNotes {
  @include bordered(red, 2px); // 调用混入，并传递两个参数
}
```

代码转换为 CSS 代码：

```css
.myArticle {
  border: 1px solid blue;
}

.myNotes {
  border: 2px solid red;
}
```

---

混入的参数也可以定义默认值：

```scss
@mixin bordered($color: blue, $width: 1px) {
  border: $width solid $color;
}
```

在包含混入时，你只需要传递需要的变量名及其值：

```scss
@mixin sexy-border($color, $width: 1in) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}
p { @include sexy-border(blue); }
h1 { @include sexy-border(blue, 2in); }
```

转换为 CSS 代码：

```css
p {
  border-color: blue;
  border-width: 1in;
  border-style: dashed; }

h1 {
  border-color: blue;
  border-width: 2in;
  border-style: dashed;
}
```

## 6.4 可变参数

有时，不能确定一个混入（mixin）或者一个函数（function）使用多少个参数，这时我们就可以使用 ... 来设置可变参数。

```scss
@mixin box-shadow($shadows...) {
      -moz-box-shadow: $shadows;
      -webkit-box-shadow: $shadows;
      box-shadow: $shadows;
}

.shadows {
  @include box-shadow(0px 4px 5px #666, 2px 6px 10px #999);
}
```

代码转换为 CSS 代码：

```css
.shadows {
  -moz-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  -webkit-box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
  box-shadow: 0px 4px 5px #666, 2px 6px 10px #999;
}
```

## 6.5 浏览器前缀使用混入

浏览器前缀使用混入也是非常方便的：

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.myBox {
  @include transform(rotate(20deg));
}
```

转换为 CSS 代码：

```css
.myBox {  
  -webkit-transform: rotate(20deg);  
  -ms-transform: rotate(20deg);  
  transform: rotate(20deg);  
}
```

# 7、 Sass @extend 与 继承

@extend 指令告诉 Sass 一个选择器的样式从另一选择器继承。

如果一个样式与另外一个样式几乎相同，只有少量的区别，则使用 @extend 就显得很有用。

【举例】

```scss
.button-basic  {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  @extend .button-basic;
  background-color: red;
}

.button-submit  {
  @extend .button-basic;
  background-color: green;
  color: white;
}
```

转换为 CSS 代码：

```css
.button-basic, .button-report, .button-submit {
  border: none;
  padding: 15px 30px;
  text-align: center;
  font-size: 16px;
  cursor: pointer;
}

.button-report  {
  background-color: red;
}

.button-submit  {
  background-color: green;
  color: white;
}
```

使用 @extend 后，我们在 HTML 按钮标签中就不需要指定多个类 class="button-basic button-report" ，只需要设置 class="button-report" 类就好了。

@extend 很好的体现了代码的复用。

# 8、Sass 函数

Sass 定义了各种类型的函数，这些函数我们可以通过 CSS 语句直接调用。

| 序号  | 函数类别                                                                                |
| --- | ----------------------------------------------------------------------------------- |
| 1   | [Sass 字符串相关函数](https://www.runoob.com/sass/sass-string-func.html)                   |
| 2   | [Sass 数字相关函数](https://www.runoob.com/sass/sass-numeric-func.html)                   |
| 3   | [Sass 列表(List)相关函数](https://www.runoob.com/sass/sass-list-func.html)                |
| 4   | [Sass 映射(Map)相关函数](https://www.runoob.com/sass/sass-map-func.html)                  |
| 5   | [Sass 选择器相关函数](https://www.runoob.com/sass/sass-selector-func.html)                 |
| 6   | [Sass Introspection 相关函数](https://www.runoob.com/sass/sass-introspection-func.html) |
| 7   | [Sass 颜色相关函数](https://www.runoob.com/sass/sass-color-func.html)                     |
