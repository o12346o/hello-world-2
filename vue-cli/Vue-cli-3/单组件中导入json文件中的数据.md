# 导入json 文件中的数据

当不需要改变时，可以通过以下这种方式导入 json 文件中的数据：

```js
import data from '@/assets/mock/1.json'

export default {
  mounted(){
    console.log(data)  
  }
}
```

此方式可以无需开启服务器，即可直接使用本地数据，打包时会将该json文件中的数据直接打包到js文件中。