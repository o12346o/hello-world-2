# echarts 基础使用

## 使用 echarts 的基本流程

```js
// 导入
import * as echarts from 'echarts'

// 初始化
const myChart = echarts.init(document.getElementById('box'));

// 配置
const option = {
    title:{},
    tooltop:{},
    legend:{},
    xAixs:{
        type:'catageory',
        data:['类型一'，'类型二','类型三']
    },
    yAixs:{},
    series:[
        {
            type:'bar',
            data:[1,2,3]
        }
    ]
};

// 使用配置
myChar.setOption(option)

// 监听窗口大小
window.addEventListener('resize', ()=>{
    // 当窗口大小改变时，echarts绘图大小改变
    myCharts.resize()
})
```