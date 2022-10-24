# 1、js正则表达式

```js
var patt = /runoob/i
```

**/runoob/i**  是一个正则表达式。

**runoob**  是一个**正则表达式主体** (用于检索)。

**i**  是一个**修饰符** (搜索不区分大小写)。

## 1.1 正则表达式修饰符

**修饰符** 可以在全局搜索中不区分大小写:

| 修饰符 | 描述                           |
| --- | ---------------------------- |
| i   | 执行对大小写不敏感的匹配。                |
| g   | 执行全局匹配（查找所有匹配而非在找到第一个匹配后停止）。 |
| m   | 执行多行匹配。                      |

## 1.2 正则表达式模式

方括号用于查找某个范围内的字符：

| 表达式    | 描述               |
| ------ | ---------------- |
| [abc]  | 查找方括号之间的任何字符。    |
| [0-9]  | 查找任何从 0 至 9 的数字。 |
| (x\|y) | 查找任何以 \| 分隔的选项。  |

元字符是拥有特殊含义的字符：

| 元字符    | 描述                            |
| ------ | ----------------------------- |
| \d     | 查找数字。                         |
| \D     | 查找非数字字符。                      |
| \s     | 查找空白字符。                       |
| \S     | 查找非空白字符。                      |
| \b     | 匹配单词边界。                       |
| \B     | 匹配非单词边界。                      |
| \uxxxx | 查找以十六进制数 xxxx 规定的 Unicode 字符。 |

量词:

| 量词  | 描述                    |
| --- | --------------------- |
| n+  | 匹配任何包含至少一个 *n* 的字符串。  |
| n*  | 匹配任何包含零个或多个 *n* 的字符串。 |
| n?  | 匹配任何包含零个或一个 *n* 的字符串。 |

# 2、JavaScript 错误

**try** 语句测试代码块的错误。

**catch** 语句处理错误。

**throw** 语句创建自定义错误。

**finally** 语句在 try 和 catch 语句之后，无论是否有触发异常，该语句都会执行。

## 2.1 语法

```js
try {
    ...    //异常的抛出
} catch(e) {
    ...    //异常的捕获与处理
} finally {
    ...    //结束处理
}
```

## 2.2 示例

```js
function myFunction() {
    var message, x;
    message = document.getElementById("message");
    message.innerHTML = "";
    x = document.getElementById("demo").value;
    try { 
        if(x == "")  throw "值为空";
        if(isNaN(x)) throw "不是数字";
        x = Number(x);
        if(x < 5)    throw "太小";
        if(x > 10)   throw "太大";
    }
    catch(err) {
        message.innerHTML = "错误: " + err;
    }
    finally {
        document.getElementById("demo").value = "";
    }
}
```

# 3、js调试

## 3.1 console.log() 方法

## 3.2 设置断点

在调试窗口中，你可以设置 JavaScript 代码的断点。

在每个断点上，都会停止执行 JavaScript 代码，以便于我们检查 JavaScript 变量的值。

在检查完毕后，可以重新执行代码（如播放按钮）。

## 3.3 debugger 关键字

**debugger** 关键字用于停止执行 JavaScript，并调用调试函数。

这个关键字与在调试工具中设置断点的效果是一样的。

如果没有调试可用，debugger 语句将无法工作。

开启 debugger ，代码在第三行前停止执行。

# 

```js
var x = 15 * 5;
debugger;
document.getElementbyId("demo").innerHTML = x;
```
