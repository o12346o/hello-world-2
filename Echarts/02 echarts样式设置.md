# echarts 样式设置

## 2.1 主题样式

在初始化时，传入字符串或对象来设置主题样式。

```js
const myChart = echarts.init(DOM节点, 'dark') // 设置主题样式为 dark
```

## 2.2 调色盘

调色盘可以在 option 中设置。

调色盘给定了一组颜色，图形、系列会自动从其中选择颜色。

可以设置全局的调色盘，也可以设置系列自己专属的调色盘。

```js
option = {
    // 全局调色盘。
    color: ['#c23531','#2f4554', '#61a0a8', '#d48265', '#91c7ae','#749f83',  '#ca8622', '#bda29a','#6e7074', '#546570', '#c4ccd3'],

    series: [{
        type: 'bar',
        // 此系列自己的调色盘。
        color: ['#dd6b66','#759aa0','#e69d87','#8dc1a9','#ea7e53','#eedd78','#73a373','#73b9bc','#7289ab', '#91ca8c','#f49f42'],
        ...
    }, {
        type: 'pie',
        // 此系列自己的调色盘。
        color: ['#37A2DA', '#32C5E9', '#67E0E3', '#9FE6B8', '#FFDB5C','#ff9f7f', '#fb7293', '#E062AE', '#E690D1', '#e7bcf3', '#9d96f5', '#8378EA', '#96BFFF'],
        ...
    }]
}
```


## 2.3 直接的样式设置

可以在 itemStyle, lineStyle, areaStyle, label等中直接设置样式。


## 2.4 高亮的样式

在鼠标悬浮到图形元素上时，一般会出现高亮的样式。默认情况下，高亮的样式是根据普通样式自动生成的。

如果要自定义高亮样式可以通过 emphasis 属性来定制：

```js
option= {
    emphasis: {
        itemStyle: {
            // 高亮时点的颜色
            color: 'red'
        },
        label: {
            show: true,
            // 高亮时标签的文字
            formatter: '高亮时显示的标签内容'
        }
    },
    series: [],
    /* 其他代码省略 */
}
```