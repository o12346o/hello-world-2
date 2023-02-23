# echarts 异步加载数据

echarts 通常数据设置在 setOption 中，如果我们需要异步加载数据，在异步获取数据后通过 setOption 填入数据和配置项就行。

```js
const myChart = echarts.init(DOM节点);

myChart.showLoading(); // 开启 loading 效果

axios.get(url).then((data)=>{

    myChart.hideLoading()； // 关闭 loading 效果

    myChart.setOption({
        series:[
            {    
    name: '异步加载数据',
    type: 'bar',
                data: data, // 使用异步数据
            }
        ]
    })；
});
```