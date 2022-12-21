# vite环境变量配置

> 环境变量：会根据当前的代码环境产生值的变化的变量叫做环境变量。



代码环境：

1. 开发环境

2. 测试环境

3. 预发布环境

4. 灰度环境

5. 生产环境

6. 等等...



例如，开发环境中请求的后端API地址和生产环境中请求的后端API不是同一个。



在 vite 中的环境变量处理：

vite 中内置了 dotenv 这个第三方库

dotenv 会自动读取 `.env` 文件，并解析这个文件中的对应环境变量，并将其注入到 process 对象下（但是 vite 考虑到和其他配置的一些冲突问题，不会直接注入到 process 对象下）。



涉及到 vite.config.js 中的一些配置：

- root

- envDir：用来配置当前环境变量的文件地址。

vite 给我们提供了一些补偿措施：

我们可以调用 vite 的 loadEnv 来手动确认 env 文件

process.cwd 方法：返回当前 node 进程的工作目录。

```
export default defineConfig(()=>{
    const env = loadEnv(mode, process.cwd(), "")
}
```

`.env`: 所有环境都需要用到的环境变量

`.env.development`: 开发环境需要用到的环境遍历（默认情况下，vite 将开发环境取名为 development）

`.env.production`: 生产环境需要用到的环境遍历（默认情况下，vite 将开发环境取名为 production）

`npm run dev --mode development`: 会将 mode 设置为 development 传递进来。

当我们调用 loadenv 时，会做以下几件事：

1. 直接找到`.env`文件，并解析其中的环境遍历，并放进一个对象里。

2. 会将传进来的 mode 这个遍历的值进行拼接`.env.development`，并根据我们提供的目录取对应的文件并进行解析，并放进一个对象。

3. 我们可以理解为
   
   ```js
   const baseEnvConfig = 读取 .env 的配置
   const modeEnvConfig = 读 env 相关配置
   const lastEnbConfig = {...baseEnvConfig, ...modeEnvConfig }
   ```

> 补充一个小知识：为什么 vite.config.js 可以书写成 esmodule 的形式，这是因为 vite 在读取 vite.config.js 时，会事先 node 解析文件语法 ，如果发现你是 esmodule 规范会直接将你的 esmodule 规范进行替换，变为 commonjs 规范。



如果是客户端，vite 会将对应的环境变量注入到 import.meta.env 里

vite 做了一个拦截，他为了防止我们将隐私性的变量直接送进 import.meta.env中，所以他做了一层拦截，如果你的环境变量不是以 `VITE_` 为前缀，就会被拦截。（可以在config文件中使用envPrefix来修改前缀）


