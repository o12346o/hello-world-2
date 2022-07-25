# HTML 简介

## HTML文档结构

```html
<!DOCTYPE html>
<html lang="zh-cn">
<head>
  <meta charset="UTF-8">
  <title>页面标题</title>
</head>
<body>

  <h1>我的第一个标题</h1>

  <p>我的第一个段落。</p>

</body>
</html>
```

### !DOCTYPE 声明

对于中文网页需要使用 `<meta charset="utf-8">`声明编码，否则会出现乱码。

```html
<!DOCTYPE html>
```

### HTML

HTML中有 head 和 body 两部分。

```html
<!DOCTYPE html>
<html>
<head></head>
<body></body>
</html>
```

#### 1、head

<head> 元素包含了所有的头部标签元素。在 <head>元素中你可以插入脚本（scripts）, 样式文件（CSS），及各种meta信息。

可以添加在头部区域的元素标签为: title, style, meta, link, script, noscript 和 base。

| 标签     | 描述                |
| ------ | ----------------- |
| head   | 定义了文档的信息          |
| title  | 定义了文档的标题          |
| base   | 定义了页面链接标签的默认链接地址  |
| link   | 定义了一个文档和外部资源之间的关系 |
| mate   | 定义了HTML文档中的元数据    |
| script | 定义了客户端的脚本文件       |
| style  | 定义了HTML文档的样式文件    |

##### title 元素

- 定义了浏览器工具栏的标题。

- 当网页添加到收藏夹时，显示在收藏夹中的标题。

- 显示在搜索引擎结果页面的标题。

##### style 元素

- 定义了文档与外部资源的关系。

- 通常用于链接到样式表。

```html
<head>
  <link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

##### meta 元素

meta标签描述了一些基本的元数据。

meta 标签提供了元数据.元数据也不显示在页面上，但会被浏览器解析。

META 元素通常用于指定网页的描述，关键词，文件的最后修改时间，作者，和其他元数据。

元数据可以使用于浏览器（如何显示内容或重新加载页面），搜索引擎（关键词），或其他Web服务。

**meta 标签- 使用实例**

为搜索引擎定义关键词:

```html
<head>
  <meta name="keywords" content="HTML, CSS, XML, XHTML, JavaScript">
</head>
```

为网页定义描述内容:

```html
<head>
  <meta name="description" content="免费 Web & 编程 教程">
</head>
```

定义网页作者:

```html
<head>
  <meta name="author" content="Runoob">
</head>
```

每30秒钟刷新当前页面:

```html
<head>
    <meta http-equiv="refresh" content="30">
</head>
```

#### 2、body

body中为网页显示内容。

```html
<!DOCTYPE html>
<html>
<head></head>
<body>
    网页显示容
</body>
</html>
```

# HTML 的各类标签

## 标题 h1~h6

```html
<h1>这是一个标题</h1>
<h2>这是一个标题</h2>
<h3>这是一个标题</h3>
<h4>这是一个标题</h4>
<h5>这是一个标题</h5>
<h6>这是一个标题</h6>
```

## 段落 p

```html
<p>这是一个段落。</p>
<p>这是另一个段落。</p>
```

## 段内换行 br

```html
<p>第一行<br/>下一行</p>
```

## 预留格式 pre

```html
<pre>
  这是一个预留格式
的段落。
</pre>
```

## 段内分组 span

```html
<p>这是一个<span>段内分组<span>段落。</p>
```

## 水平线 hr

```html
<hr/>
```

## 链接

```html
<a href="#">这是一个链接</a>
```

| 属性             | 值                                                                                                                                                             | 描述                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| download       | *filename*                                                                                                                                                    | 规定被下载的超链接目标。                                                  |
| href           | *URL*                                                                                                                                                         | 规定链接指向的页面的 URL。                                               |
| hreflang       | *language_code*                                                                                                                                               | 规定被链接文档的语言。                                                   |
| media          | *media_query*                                                                                                                                                 | 规定被链接文档是为何种媒介/设备优化的。                                          |
| referrerpolicy | - no-referrer<br>- no-referrer-when-downgrade<br>- origin<br>- origin-when-cross-origin<br>- same-origin<br>- strict-origin-when-cross-origin<br>- unsafe-url | 规定当用户单击超链接时要发送哪些引荐来源信息。                                       |
| ping           | *list_of_URLs*                                                                                                                                                | 规定以空格分隔的 URL 列表，当点击链接时，浏览器将发送带有正文 ping 的 post 请求（在后台）。通常用于跟踪。 |
| name           | *section_name*                                                                                                                                                | HTML5 中不支持。规定锚的名称。                                            |
| rel            | *text*                                                                                                                                                        | 规定当前文档与被链接文档之间的关系。                                            |
| target         | - _blank<br>- _parent<br>- _self<br>- _top<br>- *framename*                                                                                                   | 规定在何处打开链接文档。                                                  |
| type           | *MIME type*                                                                                                                                                   | 规定被链接文档的的 MIME 类型。                                            |

## 图像

```html
<img src="./loga.png" alt="图片加载失败"/>
```

| 属性     | 值             | 描述                           |
| ------ | ------------- | ---------------------------- |
| alt    | text          | 规定图像的替代文本。                   |
| src    | URL           | 规定显示图像的 URL。                 |
| width  | pixels <br/>% | 设置图像的宽度。默认单位为像素，即省略单位时单位为像素。 |
| height | pixels <br/>% | 设置图像的高度。默认单位为像素。             |

## 区域 div

```html
<div>这是一个区域</div>
```

## 无序列表 ul

```html
<ul>
  <li>html</li>
  <li>css</li>
</ul>
```

## 有序列表 ol

```html
<ol>
  <li>html</li>
  <li>css</li>
</ol>
```

## 表格 table

```html
<table>
    <tr>
        <th>表头1</th>
        <th>表头2</th>
    </tr>
    <tr>
        <td>内容</td>
        <td>内容</td>
    <tr>
</table>
```

**表格标签**

| 标签                                                        | 描述         |
| --------------------------------------------------------- | ---------- |
| [table](https://www.runoob.com/tags/tag-table.html)       | 定义表格       |
| [th](https://www.runoob.com/tags/tag-th.html)             | 定义表格的表头    |
| [tr](https://www.runoob.com/tags/tag-tr.html)             | 定义表格的行     |
| [td](https://www.runoob.com/tags/tag-td.html)             | 定义表格单元     |
| [caption](https://www.runoob.com/tags/tag-caption.html)   | 定义表格标题     |
| [colgroup](https://www.runoob.com/tags/tag-colgroup.html) | 定义表格列的组    |
| [col](https://www.runoob.com/tags/tag-col.html)           | 定义用于表格列的属性 |
| [thead](https://www.runoob.com/tags/tag-thead.html)       | 定义表格的页眉    |
| [tbody](https://www.runoob.com/tags/tag-tbody.html)       | 定义表格的主体    |
| [tfoot](https://www.runoob.com/tags/tag-tfoot.html)       | 定义表格的页脚    |

**表格属性**

| 属性                                                                                                          | 值                                                                                           | 描述               |
| ----------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ---------------- |
| [border](https://www.w3school.com.cn/tags/att_table_border.asp "HTML <table> 标签的 border 属性")                | *pixels*                                                                                    | 规定表格边框的宽度。       |
| [cellpadding](https://www.w3school.com.cn/tags/att_table_cellpadding.asp "HTML <table> 标签的 cellpadding 属性") | *pixels*<br>*%*                                                                             | 规定单元边沿与其内容之间的空白。 |
| [cellspacing](https://www.w3school.com.cn/tags/att_table_cellspacing.asp "HTML <table> 标签的 cellspacing 属性") | - *pixels*<br>- *%*                                                                         | 规定单元格之间的空白。      |
| [frame](https://www.w3school.com.cn/tags/att_table_frame.asp "HTML <table> 标签的 frame 属性")                   | - void<br>- above<br>- below<br>- hsides<br>- lhs<br>- rhs<br>- vsides<br>- box<br>- border | 规定外侧边框的哪个部分是可见的。 |
| [rules](https://www.w3school.com.cn/tags/att_table_rules.asp "HTML <table> 标签的 rules 属性")                   | - none<br>- groups<br>- rows<br>- cols<br>- all                                             | 规定内侧边框的哪个部分是可见的。 |
| [summary](https://www.w3school.com.cn/tags/att_table_summary.asp "HTML <table> 标签的 summary 属性")             | *text*                                                                                      | 规定表格的摘要。         |
| [width](https://www.w3school.com.cn/tags/att_table_width.asp "HTML <table> 标签的 width 属性")                   | - *%*<br>- *pixels*                                                                         | 规定表格的宽度。         |

**th 和 tr 的属性**

| 属性                                                                                        | 值                                           | 描述                              |
| ----------------------------------------------------------------------------------------- | ------------------------------------------- | ------------------------------- |
| [abbr](https://www.w3school.com.cn/tags/att_th_abbr.asp "HTML <th> 标签的 abbr 属性")          | *text*                                      | 规定单元格中内容的缩写版本。                  |
| [align](https://www.w3school.com.cn/tags/att_th_align.asp "HTML <th> 标签的 align 属性")       | left<br>right<br>center<br>justify<br>char  | 规定单元格内容的水平对齐方式。                 |
| [axis](https://www.w3school.com.cn/tags/att_th_axis.asp "HTML <th> 标签的 axis 属性")          | *category_name*                             | 对单元格进行分类。                       |
| [char](https://www.w3school.com.cn/tags/att_th_char.asp "HTML <th> 标签的 char 属性")          | *character*                                 | 规定根据哪个字符来进行内容的对齐。               |
| [charoff](https://www.w3school.com.cn/tags/att_th_charoff.asp "HTML <th> 标签的 charoff 属性") | *number*                                    | 规定对齐字符的偏移量。                     |
| [colspan](https://www.w3school.com.cn/tags/att_th_colspan.asp "HTML <th> 标签的 colspan 属性") | *number*                                    | 设置单元格可横跨的列数。                    |
| [headers](https://www.w3school.com.cn/tags/att_th_headers.asp "HTML <th> 标签的 headers 属性") | *idrefs*                                    | 由空格分隔的表头单元格 ID 列表，为数据单元格提供表头信息。 |
| [rowspan](https://www.w3school.com.cn/tags/att_th_rowspan.asp "HTML <th> 标签的 rowspan 属性") | *number*                                    | 规定单元格可横跨的行数。                    |
| [scope](https://www.w3school.com.cn/tags/att_th_scope.asp "HTML <th> 标签的 scope 属性")       | col<br>colgroup<br>row<br>rowgroup          | 定义将表头数据与单元数据相关联的方法。             |
| [valign](https://www.w3school.com.cn/tags/att_th_valign.asp "HTML <th> 标签的 valign 属性")    | - top<br>- middle<br>- bottom<br>- baseline | 规定单元格内容的垂直排列方式。                 |

## 表单 form

```html
<form>
    <input type="text" name="username" placeholder="用户名" />
    <input type="password" name="password" placeholder="密码" />

    <input type="submit" />
    <input type="reset" />

    <input type="radio" name="gender" value="男"/>
    <input type="radio" name="gender" value="女"/>

    <input type="checkbox" name="hobby" />
    <input type="checkbox" name="hobby" />

    <select>
        <option>看书</option>
        <option selected="selected">旅游</option>
        <option>运动</option>
        <option>购物</option>
    </select>

    <textarea cols="30" rows="10">请输入...</textarea>
</form>
```

| 属性                                                                                                              | 值                                                                                                                         | 描述                          |
| --------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------------- |
| [accept-charset](https://www.w3school.com.cn/tags/att_form_accept-charset.asp "HTML5 <form> accept-charset 属性") | *charset_list*                                                                                                            | 规定服务器可处理的表单数据字符集。           |
| [action](https://www.w3school.com.cn/tags/att_form_action.asp "HTML5 <form> action 属性")                         | *URL*                                                                                                                     | 规定当提交表单时向何处发送表单数据。          |
| [autocomplete](https://www.w3school.com.cn/tags/att_form_autocomplete.asp "HTML5 <form> autocomplete 属性")       | - on<br>- off                                                                                                             | 规定是否启用表单的自动完成功能。            |
| [enctype](https://www.w3school.com.cn/tags/att_form_enctype.asp "HTML5 <form> enctype 属性")                      | application/x-www-form-urlencoded<br/>multipart/form-data<br/>text/plain                                                | 规定在发送表单数据之前如何对其进行编码。        |
| [method](https://www.w3school.com.cn/tags/att_form_method.asp "HTML5 <form> method 属性")                         | - get<br>- post                                                                                                           | 规定用于发送 form-data 的 HTTP 方法。 |
| [name](https://www.w3school.com.cn/tags/att_form_name.asp "HTML5 <form> name 属性")                               | *form_name*                                                                                                               | 规定表单的名称。                    |
| [novalidate](https://www.w3school.com.cn/tags/att_form_novalidate.asp "HTML5 <form> novalidate 属性")             | novalidate                                                                                                                | 如果使用该属性，则提交表单时不进行验证。        |
| [rel](https://www.w3school.com.cn/tags/att_form_rel.asp "HTML <form> rel 属性")                                   | - external<br>- help<br>- license<br>- next<br>- nofollow<br>- noopener<br>- noreferrer<br>- opener<br>- prev<br>- search | 规定链接资源和当前文档之间的关系。           |
| [target](https://www.w3school.com.cn/tags/att_form_target.asp "HTML5 <form> target 属性")                         | - _blank<br>- _self<br>- _parent<br>- _top<br>- *framename*                                                               | 规定在何处打开 action URL。         |

## 注释

```html
<!-- 这是一个注释 -->
```

## 文本格式化

## HTML 文本格式化标签

| 标签     | 描述     |
| ------ | ------ |
| b      | 定义粗体文本 |
| em     | 定义着重文字 |
| i      | 定义斜体字  |
| small  | 定义小号字  |
| strong | 定义加重语气 |
| sub    | 定义下标字  |
| sup    | 定义上标字  |
| ins    | 定义插入字  |
| del    | 定义删除字  |

## HTML "计算机输出" 标签

| 标签   | 描述        |
| ---- | --------- |
| code | 定义计算机代码   |
| kbd  | 定义键盘码     |
| samp | 定义计算机代码样本 |
| var  | 定义变量      |
| pre  | 定义预格式文本   |

## HTML 引文, 引用, 及标签定义

| 标签         | 描述        |
| ---------- | --------- |
| abbr       | 定义缩写      |
| address    | 定义地址      |
| bdo        | 定义文字方向    |
| blockquote | 定义长的引用    |
| q          | 定义短的引用语   |
| cite       | 定义引用、引证   |
| dfn        | 定义一个定义项目。 |

# 属性

- HTML 元素可以设置**属性**
- 属性可以在元素中添加**附加信息**
- 属性一般描述于**开始标签**
- 属性总是以名称/值对的形式出现，**比如：name="value"**。

## HTML 全局属性

| 属性              | 描述                            |
| --------------- | ----------------------------- |
| accesskey       | 设置访问元素的键盘快捷键。                 |
| class           | 规定元素的类名（classname）            |
| contenteditable | 规定是否可编辑元素的内容。                 |
| contextmenu     | 指定一个元素的上下文菜单。当用户右击该元素，出现上下文菜单 |
| data-*          | 用于存储页面的自定义数据                  |
| dir             | 设置元素中内容的文本方向。                 |
| draggable       | 指定某个元素是否可以拖动                  |
| dropzone        | 指定是否将数据复制，移动，或链接，或删除          |
| hidden          | hidden 属性规定对元素进行隐藏。           |
| id              | 规定元素的唯一 id                    |
| lang            | 设置元素中内容的语言代码。                 |
| spellcheck      | 检测元素是否拼写错误                    |
| style           | 规定元素的行内样式（inline style）       |
| tabindex        | 设置元素的 Tab 键控制次序。              |
| title           | 规定元素的额外信息（可在工具提示中显示）          |
| translate       | 指定是否一个元素的值在页面载入时是否需要翻译        |

## Window 事件属性

针对 window 对象触发的事件（应用到 <body> 标签）。

| 属性                                                                                                  | 值      | 描述                        |
| --------------------------------------------------------------------------------------------------- | ------ | ------------------------- |
| [onafterprint](https://www.w3school.com.cn/tags/event_onafterprint.asp "HTML onafterprint 事件属性")    | script | 文档打印之后运行的脚本。              |
| [onbeforeprint](https://www.w3school.com.cn/tags/event_onbeforeprint.asp "HTML onbeforeprint 事件属性") | script | 文档打印之前运行的脚本。              |
| onbeforeunload                                                                                      | script | 文档卸载之前运行的脚本。              |
| onerror                                                                                             | script | 在错误发生时运行的脚本。              |
| onhaschange                                                                                         | script | 当文档已改变时运行的脚本。             |
| [onload](https://www.w3school.com.cn/tags/event_onload.asp "HTML onload 事件属性")                      | script | 页面结束加载之后触发。               |
| onmessage                                                                                           | script | 在消息被触发时运行的脚本。             |
| onoffline                                                                                           | script | 当文档离线时运行的脚本。              |
| ononline                                                                                            | script | 当文档上线时运行的脚本。              |
| onpagehide                                                                                          | script | 当窗口隐藏时运行的脚本。              |
| onpageshow                                                                                          | script | 当窗口成为可见时运行的脚本。            |
| onpopstate                                                                                          | script | 当窗口历史记录改变时运行的脚本。          |
| onredo                                                                                              | script | 当文档执行撤销（redo）时运行的脚本。      |
| [onresize](https://www.w3school.com.cn/tags/event_onresize.asp "HTML onresize 事件属性")                | script | 当浏览器窗口被调整大小时触发。           |
| onstorage                                                                                           | script | 在 Web Storage 区域更新后运行的脚本。 |
| onundo                                                                                              | script | 在文档执行 undo 时运行的脚本。        |
| [onunload](https://www.w3school.com.cn/tags/event_onunload.asp "HTML onunload 事件属性")                | script | 一旦页面已下载时触发（或者浏览器窗口已被关闭）。  |

## Form 事件

由 HTML 表单内的动作触发的事件（应用到几乎所有 HTML 元素，但最常用在 form 元素中）。

| 属性                                                                                   | 值      | 描述                          |
| ------------------------------------------------------------------------------------ | ------ | --------------------------- |
| [onblur](https://www.w3school.com.cn/tags/event_onblur.asp "HTML onblur 事件属性")       | script | 元素失去焦点时运行的脚本。               |
| [onchange](https://www.w3school.com.cn/tags/event_onchange.asp "HTML onchange 事件属性") | script | 在元素值被改变时运行的脚本。              |
| oncontextmenu                                                                        | script | 当上下文菜单被触发时运行的脚本。            |
| [onfocus](https://www.w3school.com.cn/tags/event_onfocus.asp "HTML onfocus 事件属性")    | script | 当元素获得焦点时运行的脚本。              |
| onformchange                                                                         | script | 在表单改变时运行的脚本。                |
| onforminput                                                                          | script | 当表单获得用户输入时运行的脚本。            |
| oninput                                                                              | script | 当元素获得用户输入时运行的脚本。            |
| oninvalid                                                                            | script | 当元素无效时运行的脚本。                |
| onreset                                                                              | script | 当表单中的重置按钮被点击时触发。HTML5 中不支持。 |
| [onselect](https://www.w3school.com.cn/tags/event_onselect.asp "HTML onselect 事件属性") | script | 在元素中文本被选中后触发。               |
| [onsubmit](https://www.w3school.com.cn/tags/event_onsubmit.asp "HTML onsubmit 事件属性") | script | 在提交表单时触发。                   |

## Keyboard 事件

| 属性                                                                                         | 值      | 描述          |
| ------------------------------------------------------------------------------------------ | ------ | ----------- |
| [onkeydown](https://www.w3school.com.cn/tags/event_onkeydown.asp "HTML onkeydown 事件属性")    | script | 在用户按下按键时触发。 |
| [onkeypress](https://www.w3school.com.cn/tags/event_onkeypress.asp "HTML onkeypress 事件属性") | script | 在用户敲击按钮时触发。 |
| [onkeyup](https://www.w3school.com.cn/tags/event_onkeyup.asp "HTML onkeyup 事件属性")          | script | 当用户释放按键时触发。 |

## Mouse 事件

由鼠标或类似用户动作触发的事件：

| 属性                                                                                            | 值      | 描述                      |
| --------------------------------------------------------------------------------------------- | ------ | ----------------------- |
| [onclick](https://www.w3school.com.cn/tags/event_onclick.asp "HTML onclick 事件属性")             | script | 元素上发生鼠标点击时触发。           |
| [ondblclick](https://www.w3school.com.cn/tags/event_ondblclick.asp "HTML ondblclick 事件属性")    | script | 元素上发生鼠标双击时触发。           |
| ondrag                                                                                        | script | 元素被拖动时运行的脚本。            |
| ondragend                                                                                     | script | 在拖动操作末端运行的脚本。           |
| ondragenter                                                                                   | script | 当元素元素已被拖动到有效拖放区域时运行的脚本。 |
| ondragleave                                                                                   | script | 当元素离开有效拖放目标时运行的脚本。      |
| ondragover                                                                                    | script | 当元素在有效拖放目标上正在被拖动时运行的脚本。 |
| ondragstart                                                                                   | script | 在拖动操作开端运行的脚本。           |
| ondrop                                                                                        | script | 当被拖元素正在被拖放时运行的脚本。       |
| [onmousedown](https://www.w3school.com.cn/tags/event_onmousedown.asp "HTML onmousedown 事件属性") | script | 当元素上按下鼠标按钮时触发。          |
| [onmousemove](https://www.w3school.com.cn/tags/event_onmousemove.asp "HTML onmousemove 事件属性") | script | 当鼠标指针移动到元素上时触发。         |
| [onmouseout](https://www.w3school.com.cn/tags/event_onmouseout.asp "HTML onmouseout 事件属性")    | script | 当鼠标指针移出元素时触发。           |
| [onmouseover](https://www.w3school.com.cn/tags/event_onmouseover.asp "HTML onmouseover 事件属性") | script | 当鼠标指针移动到元素上时触发。         |
| [onmouseup](https://www.w3school.com.cn/tags/event_onmouseup.asp "HTML onmouseup 事件属性")       | script | 当在元素上释放鼠标按钮时触发。         |
| onmousewheel                                                                                  | script | 当鼠标滚轮正在被滚动时运行的脚本。       |
| onscroll                                                                                      | script | 当元素滚动条被滚动时运行的脚本。        |

## Media 事件

由媒介（比如视频、图像和音频）触发的事件（适用于所有 HTML 元素，但常见于媒介元素中，比如 audio、embed、img、object、video。

| 属性                 | 值      | 描述                                    |
| ------------------ | ------ | ------------------------------------- |
| onabort            | script | 在退出时运行的脚本。                            |
| oncanplay          | script | 当文件就绪可以开始播放时运行的脚本（缓冲已足够开始时）。          |
| oncanplaythrough   | script | 当媒介能够无需因缓冲而停止即可播放至结尾时运行的脚本。           |
| ondurationchange   | script | 当媒介长度改变时运行的脚本。                        |
| onemptied          | script | 当发生故障并且文件突然不可用时运行的脚本（比如连接意外断开时）。      |
| onended            | script | 当媒介已到达结尾时运行的脚本（可发送类似“感谢观看”之类的消息）。     |
| onerror            | script | 当在文件加载期间发生错误时运行的脚本。                   |
| onloadeddata       | script | 当媒介数据已加载时运行的脚本。                       |
| onloadedmetadata   | script | 当元数据（比如分辨率和时长）被加载时运行的脚本。              |
| onloadstart        | script | 在文件开始加载且未实际加载任何数据前运行的脚本。              |
| onpause            | script | 当媒介被用户或程序暂停时运行的脚本。                    |
| onplay             | script | 当媒介已就绪可以开始播放时运行的脚本。                   |
| onplaying          | script | 当媒介已开始播放时运行的脚本。                       |
| onprogress         | script | 当浏览器正在获取媒介数据时运行的脚本。                   |
| onratechange       | script | 每当回放速率改变时运行的脚本（比如当用户切换到慢动作或快进模式）。     |
| onreadystatechange | script | 每当就绪状态改变时运行的脚本（就绪状态监测媒介数据的状态）。        |
| onseeked           | script | 当 seeking 属性设置为 false（指示定位已结束）时运行的脚本。 |
| onseeking          | script | 当 seeking 属性设置为 true（指示定位是活动的）时运行的脚本。 |
| onstalled          | script | 在浏览器不论何种原因未能取回媒介数据时运行的脚本。             |
| onsuspend          | script | 在媒介数据完全加载之前不论何种原因终止取回媒介数据时运行的脚本。      |
| ontimeupdate       | script | 当播放位置改变时（比如当用户快进到媒介中一个不同的位置时）运行的脚本。   |
| onvolumechange     | script | 每当音量改变时（包括将音量设置为静音）时运行的脚本。            |
| onwaiting          | script | 当媒介已停止播放但打算继续播放时（比如当媒介暂停已缓冲更多数据）运行脚本  |
