CSS 使用变量

```css
:root { /* 在 :root 中创建变量 */
    bgColor: red; /* 变量名: 变量值 */
    fontColor: blue;
}

.box {
    background: var(--bgColor); /* 使用变量，var(--变量名) */
}
```


