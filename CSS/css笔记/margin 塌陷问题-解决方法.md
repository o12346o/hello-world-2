# 解决 margin 塌陷问题

场景：互相嵌套 的 块级元素，子元素 margin-top 影响到 父元素的位置，

结果：父元素一起往下移动

解决方法：

1. 给父元素设置 border-top 或 padding-top

2. 给父元素设置 overflow: hidden （最简单）

3. 转为行内元素

4. 设置浮动

5. 设置定位
