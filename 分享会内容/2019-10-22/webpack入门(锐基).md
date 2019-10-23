# 一、关于 webpack

### 1.什么是webpack

> Webpack是基于**Node.js**开发出来的一个前端项目构建工具；
>
> 本质上，**webpack** 是一个现代 JavaScript 应用程序的**静态模块打包工具**。当 webpack 处理应用程序时，它会在内部构建一个 [依赖图(dependency graph)](https://webpack.docschina.org/concepts/dependency-graph/)，此依赖图会映射项目所需的每个模块，并生成一个或多个 *bundle*。

### 2.为什么要使用 webpack

1. 网页**加载速度慢** (许多二次请求)
2. ##### 需要处理错综复杂的依赖关系 

------

二、webpack 的使用

### 1. 初始化项目目录

在根项目中执行 `npm init` 或  `npm init -y`命令，初始化项目目录环境生成 `package.json`, 该文件存放这当前目录的<u>相关消息，包括版本号、开发者、开发环境依赖、生产环境依赖</u>等，可以在 `scripts`构建 webpack 命令

### 2. 安装 webpack（安装之前需要先安装 **Node**环境）

​	1) 	`npm i webpack webpack-cli -g`全局安装

​	2)	 在项目的根目录中运行 `npm install --save-dev webpack webpack-cli` 或 `yarn add webpack webpack-cli -D`

> npm install xxx **-S**    即    npm install xxx **--save**    写入**dependencies**
>
> npm install xxx **-D**    即    npm install xxx **--save-dev**  写入**devDependencies**
>
> devDependencies 里面的插件只用于**开发环境**，不用于生产环境
>
> dependencies 是需要发布到**生产环境**的



### 3. 基础配置

> 在项目目录下创建 `src`目录，并在此文件夹创建 `index.js`，这是 webpack4 构建的**默认**入口文件
>
> 在根目录创建 `webpack.config.js` 配置文件：如下

`webpack.config.js`

```js
const path = require('path')
// 由于 webpack 是基于 Node 环境的，所以同样采用 Node 语法
// 通过 Node 中的模块操作，向外暴露一个配置对象
module.exports = {
    entry:'', // 打包入口文件，多页面也可以写成对象
    output:{  // 打包出口文件
        path: path.resolve(__dirname, 'dist'), // 指定打包好的文件输出到目录中去
        filename: 'bundle.js' // 这是指定输出文件名
    },
    module:{ // 配置第三方 loader 模块的
      rules:[] // 配置各种loader规则  
    },
    plugins:[], // 配置插件
    devServer:{ // 配置开发静态 http 服务
        
    }
}
```

`package.json`

```js
{
    //...
    "scripts":{
        // 配置运行命令
        "dev": "webpack --mode development", // 文件不会被压缩,
        "build": "webpack --mode production" // 文件会被压缩
    }
    //...
}
```



### 4.基本插件

#### 4.1 webpack-dev-server 

> 安装这个功能来实现自动打包编译的功能
>
> webpack-dev-server 帮我们打包生成的 bundle.js 文件并没有存放到实际的物理磁盘上，而是**托管到了电脑的内存**中。因此在项目目录中找不到这个打包好的 bundle.js 文件（**注意：你启动webpack-dev-server后，你在目标文件夹中是看不到编译后的文件的,实时编译后的文件都保存到了内存当中。因此使用webpack-dev-server进行开发的时候都看不到编译后的文件**）

1. 安装`yarn add webpack-dev-server -D`（由于是在项目中（**本地安装**）的 webpack-dev-server，所以**无法直接在终端中直接运行**，只有那些安装到全局 `-g` 的工具，才能在终端中正常执行）

2. `webpack.config.js`配置

   ```js
   // 启动热更新的 第二步
   const webpack = require('webpack'); // 引入webpack
   
   module.exports = {
       devServer: {
           contentBase: path.resolve(__dirname, 'dist'), // contentbase代表 html 页面所在的相对目录，如果我们不配置项，devServer默认html所在的目录就是项目的根目录
           port: 3000, // 端口号
           open: true, // 自动打开浏览器
           hot: true // 开启热更新的 第一步
       },
       plugins:[
           // HotModuleReplacementPlugin 是 webpack 的
           new webpack.HotModuleReplacementPlugin() // new 一个热更新的模块对象，启用热更新的第三步
       ]
   }
   
   ```

   由于配置了 webpack-dev-server, `package.json`文件可配置如下

   ```js
   {
       //...
       "scripts":{
           // 配置运行命令
           "dev": "webpack-dev-server --mode development", // 文件不会被压缩,
           "build": "webpack --mode production" // 文件会被压缩
       }
       //...
   }
   ```

   

#### 4.2 html-webpack-plugin

> 自动在**内存中**根据指定页面生成一个内存中的页面
>
> **使用了该插件之后，不再需要手动处理 bundle.js 的引用路径了，因为该插件会自动创建合适的 script 标签并且引用了正确的路径**

1. 安装 `yarn add html-webpack-plugin -D`

2.  `webpack.config.js`

   ```js
   const htmlWebpackPlugin = require('html-webpack-plugin');
   // 只要是插件都要插入到 plugins 数组
   
   module.exports = {
       plugins:[
           new htmlWebpackPlugin({ // 创建一个 在内存中生成 html 页面的插件
               template: path.join(__dirname, 'public', 'index.html'), // 指定模板页面，将来会根据指定的页面路径去生成内存中的页面
               filename: 'index.html', // 指定生成的页面的名称
               hash: true, // 给生成的 js 文件一个独特的 hash 值
               // chunk: []  
           })
       ]
   }
   ```

#### 4.3 clean-webpack-plugin

> 每次打包之前**删除 dist** 文件夹，**重新**生成 dist 文件夹，从而清除冗余文件

1. 安装 `yarn add clean-webpack-plugin -D`

2.  `webpack.config.js`

   ```js
   let CleanWebpackPlugin = require('clean-webpack-plugin'); // 导入插件
   
   module.exports = {
       plugins:[
           new CleanWebpackPlugin('./dist')
       ]
   }
   ```

   

### 5. loader 配置

> webpack **默认只能**打包处理 JS 类型的文件，无法处理其他文件，需要手动安装一些合适的第三方 loader 加载器

#### 5.1 打包处理 .css文件

> 只用 **link** 标签引入 css 文件会引起 **ajax 请求**，项目开发中不建议

 1. 安装对应的 loader `yarn add style-loader css-loader -D`

 2. `webpack.config.js`配置

    ```js
    module.exports = {
        module: { // 配置第三方 loader 模块的
            rules:[ // 第三方模块的匹配规则
                // 对于引入的文件带有非js的.xxx 后缀
                {
                    test: /\.css$/, // 正则匹配文件
                    use: ['style-loader', 'css-loader'] // 使用对应的加载器（调用从右到左，处理结果交给前面的loader）
                    // css-loader: 解析 @import 等css语法的
                    // style-loader: 将css插入到head标签中
                },
                {
                    
                    
                }
            ]
        }
    }
    ```

#### 5.2 打包处理 .less 文件

1. 安装 `yarn add less-loader less -D`,

   less 只是 less-loader 内部依赖的，不需要去配置

2. `webpack.config.js`

   ```js
   module.exports = {
       module: {
           rules:[
               {
                   test: /\.less$/, // 正则匹配文件
                   use: ['style-loader', 'css-loader','less-loader'] // 使用对应的加载器（调用从右到左，处理结果交给前面的loader）
               }
           ]
       }
   }
   ```

#### 5.3 打包处理 .scss 文件

1. 安装 `yarn add sass-loader node-sass -D`,

   node-sass 是 loader 的内部依赖，不需要配置(最好不要用npm安装)

2. `webpack.config.js`

   ```js
   module.exports = {
       module: {
           rules:[
               {
                   test: /\.scss$/, // 正则匹配文件
                   use: ['style-loader', 'css-loader','sass-loader'] // 使用对应的加载器（调用从右到左，处理结果交给前面的loader）
               }
           ]
       }
   }
   ```

#### 5.4 打包处理 图片、文件

> **如果页面图片较多，发很多http请求，会降低页面性能**。这个问题可以通过url-loader解决。url-loader会将引入的图片编码，生成dataURl并将其打包到文件中，最终只需要引入这个dataURL就能访问图片了。
>
> 当然，如果图片**较大，编码会消耗性能**。因此url-loader提供了一个limit参数，**小于limit字节的文件会被转为DataURl，大于limit的还会使用file-loader进行copy**

1. 安装 `yarn add url-loader -D`

2. `webpack.config.js`

   ```js
   module.exports = {
       module: {
           rules:[
               {
                   test: /\.(jpg|png|git|bmp|jpeg)$/, // 正则匹配文件
                   use: [
                       {
                           loader:'url-loader',
                           options:{
                               limit: 8000
                               // 如果图片字节数小于 limit 字节数，则会被转为base64字符串
                               // 否则用 file-loader来处理
                               // 则加了该参数后 url-loader 依赖于 file-loader
                           }
                   	}
                   ]// 使用对应的加载器
               }
           ]
       }
   }
   ```

   

#### 5.5 打包处理图片、字体等文件

> 在css文件中定义background的属性或者在html中引入image的src，我们知道在webpack打包后这些图片会打包至定义好的一个文件夹下，**和开发时候的相对路径会不一样，这就会导致导入图片路径的错误**。而file-loader正是为了解决此类问题而产生的，**他修改打包后图片的储存路径，再根据配置修改我们引用的路径，使之对应引入**
>
> **与url-loader的联系：**url-loader内部封装了file-loader，**即url-loader是file-loader 的加强版，可以使用limit参数**，url-loader不依赖于file-loader，即使用url-loader时，只需要安装url-loader即可，不需要安装file-loader。它们的参数也不同

1. 安装 `yarn add file-loader -D`

2. `webpack.config.js`

   ```js
   module.exports = {
       module: {
           rules:[
               {
                   test: /\.(jpg|png|git|bmp|jpeg)$/, // 正则匹配图片文件
                   use:{
                       loader: 'file-loader',
                       options:{
                           name: '[name]-[hash:8].[ext]',
                           publicPath: '/'
                       }
                   }
               },
               {                
                   test: /\.(ttf|woff2|woff|eot|svg)$/, // 正则匹配字体文件
                   use: 'file-loader' // 处理字体文件
               }
           ]
       }
   }
   ```

#### 5.6 配置转义插件 babel

> Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中

1. 安装  `yarn add babel-loader @babel/core @babel/preset-env -D` 

   - @babel/core: babel 的核心模块
   - @babel/preset-env: 可以把标准的语法转换成低级的语法

2. `webpack.config.js`

   ```js
   module.exports = {
       module: {
           rules:[
               {
                   test: /\.js$/, // 正则匹配js文件
                   exclude: /node_modules/, // 排除项,
                   use: {
                   	loader: 'babel-loader',
                        options: {
                           presets: ['@babel/preset-env'],
                           plugins:[]
                        }
                   }
                   
               }
           ]
       }
   }
   ```

   
