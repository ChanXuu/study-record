#  webpack基础

##  webpack 安装

```javascript
npm install webpack --global                // 安装全局webpack命令
npm install webpack webpack-cli --save-dev  // 安装本地项目模块

// install    可简写为i,
// --global   可简写为-g
// --save     可简写为-S
// --save-dev 可简写为-D

```

##  webpack可以0配置

- 打包工具 >输出结果为(js模块)

##  手动配置

- 默认配置文件为webpack.config.js

  ```javascript
  //用node 写法
  
  //node的path模块
  let path = require('path')
  
  module.exports = {
      mode:'development',//模式 两种 production  development
      entry: './src/index.js', //入口
      output: {
          filename: 'bundle.js', //打包后文件名
          path: path.resolve(__dirname,'dist'), //路径必须是个绝对路径
      }
  }
  ```



##  构建本地服务

- **webpack-dev-server配置本地服务器**

  - `npm install webpack-dev-server -D`

- * **devServer配置项**

  - **contentBase：**该配置项指定了服务器资源的根目录，如果不配置contentBase的话，那么contentBase默认是当前执行的目录,一般是项目的根目录
  - **post：**指定了开启服务器的端口号，默认为8080
  - **host：**配置 DevServer的服务器监听地址，默认为 127.0.0.1
  - **headers：**该配置项可以在HTTP响应中注入一些HTTP响应头。例如：

  ```javascript
      headers: {
        'aa': '123'
      }
  ```

  - **historyApiFallback：**该配置项属性是用来应对返回404页面时定向跳转到特定页面的。一般是应用在单页应用，比如在访问路由时候，访问不到该路由的时候，通过该配置项，设置属性值为true的时候，会自动跳转到 index.html下。当然我们也可以手动通过 正则来匹配路由

  ```javascript
      // 跳到index.html页面 
      historyApiFallback: true
  
      // 使用正则来匹配路由
      historyApiFallback: {
        rewrites: [
          { from: /^\/user/, to: '/user.html' },
          { from: /^\/home/, to: '/home.html' }
        ]
      }
  
  ```

  

  - **hot：**该配置项是指模块替换换功能，DevServer 默认行为是在发现源代码被更新后通过自动刷新整个页面来做到实时预览的，但是开启模块热替换功能后，它是通过在不刷新整个页面的情况下通过使用新模块替换旧模块来做到实时预览的。
  - **proxy :** 有时候我们使用webpack在本地启动服务器的时候，由于我们使用的访问的域名是 http://localhost:8081 这样的，但是我们服务端的接口是其他的，可以通过该配置来解决跨域的问题

  ```javascript
  // 假设服务端接口域名为：http://www.baidu.com
  proxy: {
    '/api': {
      target: 'http://www.baidu.com', // 目标接口的域名
      // secure: true,  // https 的时候 使用该参数
      changeOrigin: true,  // 是否跨域
      pathRewrite: {
        '^/api' : ''  // 重写路径
      }
    }
  }
  ```

 

  - **inline：**设置为true，当源文件改变时会自动刷新页面
  - **open：**该属性用于DevServer启动且第一次构建完成时，自动使用我们的系统默认浏览器去打开网页。
  - **compress：**配置是否启用 gzip 压缩，boolean 类型，默认为 false
  - **overlay：**该属性是用来在编译出错的时候，在浏览器页面上显示错误。该属性值默认为false，需要的话，设置该参数为true



## Loaders

- **作用**

  ​     通过不同的loader，webpack有能力调用外部的脚本或工具，实现对不同格式的文件的处理，例如把scss转为css，将ES66、ES7等语法转化为当前浏览器能识别的语法，将JSX转化为js等多项功能。Loaders需要单独安装并且需要在webpack.comfig.js中的modules配置项下进行配置

- **配置**

## Plugins

- **作用**

  插件（Plugins）是用来拓展Webpack功能的，它们会在整个构建过程中生效，执行相关的任务。
  Loaders和Plugins常常被弄混，但是他们其实是完全不同的东西，可以这么来说，loaders是在打包构建过程中用来处理源文件的（JSX，Scss，Less..），一次处理一个，插件并不直接操作单个文件，它直接对整个构建过程其作用。

- **配置**


- ##路径别名##
```
//在vue.config.js中
chainWebpack: config => {
    config.resolve.alias
        .set('@', resolve('src'))
        .set('./@assets', resolve('src/assets'))
        .set('@components', resolve('src/components'))
}
```

