# 混合背景图片与背景颜色

```css
div{
      width: 200px;
      height: 200px;
      background-image: url('./04.png');
      background-size: cover;
      background-color: rgba(0,0,0,0.4);
      /*背景图片优先级高于背景颜色，默认情况下背景图片在背景颜色上方，会遮盖背景颜色*/
      background-blend-mode:multiply; /*以某种方式混合背景图片和颜色*/
}
```


