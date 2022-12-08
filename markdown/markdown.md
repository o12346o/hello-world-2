<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=2 orderedList=false} -->

<!-- code_chunk_output -->

- [Markdown 基本教程](#markdown-基本教程)
  - [一、标题](#一-标题)
  - [二、段落](#二-段落)
  - [三、引用区块](#三-引用区块)
  - [四、列表](#四-列表)
  - [五、代码](#五-代码)
  - [六、链接](#六-链接)
  - [七、图片](#七-图片)
  - [八、字符转义](#八-字符转义)
  - [九、内嵌 HTML 标签](#九-内嵌-html-标签)
- [扩展教程](#扩展教程)
  - [一、表格](#一-表格)
  - [二、围栏代码块](#二-围栏代码块)
  - [三、高级技巧](#三-高级技巧)

<!-- /code_chunk_output -->

# Markdown 基本教程

（<kbd>crtl</kbd>+<kbd>shift</kbd>+<kbd>v</kbd>预览，非实时）

（安装 Markdown Preview Enhanced 插件）

（英文输入模式下 <kbd>ctrl</kbd> + <kbd>k</kbd> 放掉，然后按 <kbd>v</kbd> 打开实时预览）

（ <kbd>Ctrl</kbd> + <kbd>Shift</kbd> + <kbd>P</kbd> 调出主命令框，输入 Markdown，选择则边栏预览）

（在预览时， <kbd>esc</kbd> 打开索引侧边栏）

## 一、标题

mk表格有两种格式。

### 1、 使用 = 和 - 标记一级和二级标题

> 一级标题
> =======
> 
> 二级标题
> -------

    一级标题
    =======
    二级标题
    -------

### 2、 使用 # 号标记

> # 一级标题
> 
> ## 二级标题
> 
> ### 三级标题
> 
> #### 四级标题
> 
> ##### 五级标题
> 
> ###### 六级标题

    # 一级标题
    ## 二级标题
    ### 三级标题
    #### 四级标题
    ##### 五级标题
    ###### 六级标题

## 二、段落

### 1、 段落

段落的换行是使用两个以上空格加上回车，或者使用一个空行表示开始一个新的段落。  

> 段落一  
> 段落二

    段落一  
    段落二

或

    段落一
    
    段落二

### 2、字体

一个星号或底线表示斜体，两个表示粗体，三个表示粗斜体。

> *斜体文本*  
> _斜体文本_  
> **粗体文本**  
> __粗体文本__  
> ***粗斜体文本***  
> ___粗斜体文本___  

    *斜体文本*  
    _斜体文本_  
    **粗体文本**  
    __粗体文本__  
    ***粗斜体文本***  
    ___粗斜体文本___  

### 3、分隔线

在一行中使用三个以上的星号、减号、底线，行内不能有其他东西。

> ***
> 
> * * *
> 
> *****
> 
> - - -
> 
> ----------

    ***
    
    * * *
    
    *****
    
    - - -
    
    ----------

### 4、删除线

如果段落上的文字要添加删除线，只需要在文字的两端加上两个波浪线 <kbd>~~</kbd> 即可。

> ~~BAIDU.COM~~

    ~~BAIDU.COM~~

### 5、下划线

下划线可以通过 HTML 的 u 标签来实现。

> <u>带下划线文本</u>

    <u>带下划线文本</u>

### 6、脚注

脚注是对文本的补充说明。

创建脚注参考，请在方括号（`[^1]`）内添加插入符号和标识符。标识符可以是数字或单词，但不能包含空格或制表符。

在括号内使用另一个插入符号和数字添加脚注，并用冒号和文本（`[^1]: My footnote.`）。

> 你好[^1]
> 
> 欢迎光临[^2]
> 
> [^1]:脚注内容
> 
> [^2]:欢迎光临，祝你学习愉快

    你好[^1]
    
    欢迎光临[^2]
    
    [^1]:脚注内容
    
    [^2]:欢迎光临，祝你学习愉快

## 三、引用区块

### 1、多个段落的块引用

> 段落一
> 
> 段落二
> 
> 段落三

    > 段落一
    > 
    > 段落二
    > 
    > 段落三

### 2、嵌套块引用

> 段落一
> 
> > 嵌套的段落二
> 
> 段落三

    > 段落一
    >
    >> 嵌套的段落二
    > 
    > 段落三

### 3、带有其它元素的块引用

> #### The quarterly results look great!
> 
> - Revenue was off the chart.
> 
> - Profits were higher than ever.
>   
>   *Everything* is going according to **plan**.

    #### The quarterly results look great!
    
    - Revenue was off the chart.
    - Profits were higher than ever.
    
    *Everything* is going according to **plan**.

## 四、列表

### 1、有序列表

在每个列表项前添加数字并紧跟一个英文句点，然后是一个空格。数字不必按数学顺序排列，但是列表应当以数字 1 起始。

> 1. 第一项
> 2. 第二项
> 3. 第三项

    1. 第一项
    2. 第二项
    3. 第三项

### 2、无序列表

要创建无序列表，请在每个列表项前面添加破折号 (-)、星号 (*) 或加号 (+) 。缩进一个或多个列表项可创建嵌套列表。

> - First item
> - Second item
> - Third item
>   - Indented item
>   - Indented item
> - Fourth item

    - First item
    - Second item
    - Third item
        - Indented item
        - Indented item
    - Fourth item

### 3、在列表中嵌套其他元素

> 1. First item
> 2. Second item
> 3. Third item
>    - Indented item
>    - Indented item
> 4. Fourth item

    1. First item
    2. Second item
    3. Third item
        - Indented item
        - Indented item
    4. Fourth item

## 五、代码

### 1、反引号代码

要将单词或短语表示为代码，请将其包裹在反引号 ` 中。

> At the command prompt, type `<p>nano</p>`.

    At the command prompt, type `<p>nano</p>`.

### 2、转义反引号

如果你要表示为代码的单词或短语中包含一个或多个反引号，则可以通过将单词或短语包裹在双反引号``中。

> ``Use `code` in your Markdown file.``

    ``Use `code` in your Markdown file.``

### 3、代码块

要创建代码块，请将代码块的每一行缩进至少四个空格或一个制表符。

代码块前面必须有换行。

     <html>
      <head>
      </head>
    </html>

### 4、使用 ``` 包裹代码块

也可以用 ``` 包裹一段代码，并指定一种语言（也可以不指定）

```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```

    ```javascript
    $(document).ready(function () {
        alert('RUNOOB');
    });
    ```

## 六、链接

### 1、超链接语法

超链接代码为`[超链接显示名](超链接地址 "超链接title")`

> 这是一个链接 [Markdown语法](https://markdown.com.cn)。

    这是一个链接 [Markdown语法](https://markdown.com.cn)。

### 2、给链接添加 title

链接title是当鼠标悬停在链接上时会出现的文字，这个title是可选的，它放在圆括号中链接地址后面，跟链接地址之间以空格分隔。

> 这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。

    这是一个链接 [Markdown语法](https://markdown.com.cn "最好的markdown教程")。

### 3、网址和Email地址

使用尖括号可以很方便地把URL或者email地址变成可点击的链接。

> <https://markdown.com.cn>
> 
> <fake@example.com>

    <https://markdown.com.cn>
    <fake@example.com>

### 4、带格式化的链接

强调 链接, 在链接语法前后增加星号。 要将链接表示为代码，请在方括号中添加反引号。

> I love supporting the **[EFF](https://eff.org)**.
> 
> This is the *[Markdown Guide](https://www.markdownguide.org)*.
> 
> See the section on [`code`](#code).

    I love supporting the **[EFF](https://eff.org)**.
    This is the *[Markdown Guide](https://www.markdownguide.org)*.
    See the section on [`code`](#code).

### 5、引用类型链接

引用样式链接是一种特殊的链接，它使URL在Markdown中更易于显示和阅读。参考样式链接分为两部分：与文本保持内联的部分以及存储在文件中其他位置的部分，以使文本易于阅读。

我们可以通过变量来设置一个链接，变量赋值在文档末尾进行。

**(1)链接的第一部分格式**

> [baidu][1]  
> 
> [baidu] [1]    

以下示例格式对于链接的第一部分效果相同，任选一种即可

    [hobbit-hole][1]
    [hobbit-hole] [1]

**(2) 链接的第二部分格式**

<!-- > [1]: https://www.baidu.com  -->

> [1]: https://www.baidu.com "百度"  
> [1]: https://www.baidu.com '百度'  
> [1]:https://www.baidu.com (百度)  
> [1]: <https://www.baidu.com> "百度"  
> [1]: <https://www.baidu.com> '百度'  
> [1]: <https://www.baidu.com> (百度)  

以下示例格式对于链接的第二部分效果相同,任选一种即可

    [1]: https://www.baidu.com "百度"  
    [1]: https://www.baidu.com '百度'  
    [1]:https://www.baidu.com (百度)  
    [1]: <https://www.baidu.com> "百度"  
    [1]: <https://www.baidu.com> '百度'  
    [1]: <https://www.baidu.com> (百度)  

## 七、图片

### 1、插入图片

语法代码：`![图片alt](图片链接 "图片title")`。

> ![这是图片](https://markdown.com.cn/assets/img/philly-magic-garden.9c0b4415.jpg "Magic Gardens")

    ![这是图片](https://markdown.com.cn/assets/img/philly-magic-garden.9c0b4415.jpg "Magic Gardens")

### 2、链接图片

语法代码：`[![图片alt](图片链接 "图片title")](链接)`

> [![沙漠中的岩石图片](https://markdown.com.cn/assets/img/shiprock.c3b9a023.jpg "markdown官方教程")](https://markdown.com.cn)

    [![沙漠中的岩石图片](https://markdown.com.cn/assets/img/shiprock.c3b9a023.jpg "markdown官方教程")](https://markdown.com.cn)

## 八、字符转义

### 1、反斜杠

使用“\”转义字符，进行转义。

> 转义前：**加粗**
> 转义后：\*\*加粗\*\*

```
\#
转义前：**加粗**
转义后：\*\*加粗\*\*
```

### 2、特殊字符自动转义

在 HTML 文件中，有两个字符需要特殊处理： < 和 & 。 < 符号用于起始标签，& 符号则用于标记 HTML 实体，如果你只是想要使用这些符号，你必须要使用实体的形式，像是 `&lt;`和 `&amp;`。

著作权符号

> &copy;

    ©

**自动转换**

如果你使用 & 符号的作为 HTML 实体的一部分，那么它不会被转换，而在其它情况下，它则会被转换成 `&amp;`。

> AT&T
> 
> 自动转换为
> 
> AT`&amp;`T

## 九、内嵌 HTML 标签

对于 Markdown 涵盖范围之外的标签，都可以直接在文件里面用 HTML 本身。如需使用 HTML，不需要额外标注这是 HTML 或是 Markdown，只需 HTML 标签添加到 Markdown 文本中即可。

### 1、行级內联标签

> This **word** is bold. This <em>word</em> is italic.

    This **word** is bold. This <em>word</em> is italic.

### 2、区块标签

> This is a regular paragraph.
> 
> <table>
>   <tr>
>    <th>标题一</th>
>    <th>标题二</th>
>    <th>标题三</th>
>  </tr>
>  <tr>
>    <td>Foo</td>
>    <td>Foo</td>
>    <td>Foo</td>
>  </tr>
>  <tr>
>    <td>Foo</td>
>    <td>Foo</td>
>    <td>Foo</td>
>  </tr>
> </table>
> 
> <p>This is another regular paragraph.</p>

    This is a regular paragraph.
    
        <table>
      <tr>
       <th>标题一</th>
       <th>标题二</th>
       <th>标题三</th>
     </tr>
     <tr>
       <td>Foo</td>
       <td>Foo</td>
       <td>Foo</td>
     </tr>
     <tr>
       <td>Foo</td>
       <td>Foo</td>
       <td>Foo</td>
     </tr>
    </table>
    
    <p>This is another regular paragraph.</p>

---

# 扩展教程

## 一、表格

### 1、添加表格

要添加表，请使用三个或多个连字符（---）创建每列的标题，并使用管道（|）分隔每列。您可以选择在表的任一端添加管道。

> | Syntax    | Description |
> | --------- | ----------- |
> | Header    | Title       |
> | Paragraph | Text        |

    | Syntax      | Description |
    | ----------- | ----------- |
    | Header      | Title       |
    | Paragraph   | Text        |

单元格宽度可以变化，如下所示。呈现的输出将看起来相同。

> | Syntax    | Description |
> | --------- | ----------- |
> | Header    | Title       |
> | Paragraph | Text        |

    | Syntax | Description |
    | --- | ----------- |
    | Header | Title |
    | Paragraph | Text |

### 2、表格对齐

您可以通过在标题行中的连字符的左侧，右侧或两侧添加冒号（:），将列中的文本对齐到左侧，右侧或中心。

> | Syntax    | Description | Test Text   |
> |:--------- |:-----------:| -----------:|
> | Header    | Title       | Here's this |
> | Paragraph | Text        | And more    |

    | Syntax      | Description | Test Text     |
    | :---        |    :----:   |          ---: |
    | Header      | Title       | Here's this   |
    | Paragraph   | Text        | And more      |

### 3、格式化表格中的文字

您可以在表格中设置文本格式。例如，您可以添加链接，代码（仅反引号（`）中的单词或短语，而不是代码块）和强调。

您不能添加标题，块引用，列表，水平规则，图像或HTML标签。

### 4、在表中转义管道字符

您可以使用表格的HTML字符代码（`&#124;`）在表中显示竖线（`|`）字符。

## 二、围栏代码块

Markdown基本语法允许您通过将行缩进四个空格或一个制表符来创建代码块。如果发现不方便，请尝试使用受保护的代码块。根据Markdown处理器或编辑器的不同，您将在代码块之前和之后的行上使用三个反引号（(```）或三个波浪号（~~~）。

> ```
> {
>   "firstName": "John",
>   "lastName": "Smith",
>   "age": 25
> }
> ```

    ```
    {
      "firstName": "John",
      "lastName": "Smith",
      "age": 25
    }
    ```

**语法高亮**
许多Markdown处理器都支持受围栏代码块的语法突出显示。使用此功能，您可以为编写代码的任何语言添加颜色突出显示。要添加语法突出显示，请在受防护的代码块之前的反引号旁边指定一种语言。

> ```json
> {
>   "firstName": "John",
>   "lastName": "Smith",
>   "age": 25
> }
> ```

    ```json
    {
      "firstName": "John",
      "lastName": "Smith",
      "age": 25
    }
    ```

## 三、高级技巧

### 1. 支持HTML元素

支持的HTML元素有：`<kbd>、<b>、<i>、<em>、<sup>、<br>`等

> 使用 <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Del</kbd> 重启电脑

    使用 <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>Del</kbd> 重启电脑

### 2. 公式

Markdown Preview Enhanced 使用 KaTeX 或者 MathJax 来渲染数学表达式。

KaTeX 拥有比 MathJax 更快的性能，但是它却少了很多 MathJax 拥有的特性。你可以查看 KaTeX supported functions/symbols 来了解 KaTeX 支持那些符号和函数。

默认下的分隔符：

+ `$...$` 或者 `\(...\)` 中的数学表达式将会在行内显示。
+ `$$...$$` 或者 `\[...\]` 或者 ```math 中的数学表达式将会在块内显示。

> $f(x)=sin(x)+12$
> $$\sum_{n=1}^{10} n $$

    $f(x)=sin(x)+12$
    $$\sum_{n=1}^{10} n $$
