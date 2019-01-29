# React 基础

## 相关地址
* [官网][react]
* [中文官网][react2]
## React 简介

### 特点

1.`声明式的视图层`,他采用的是JavaScript(JSX)语法来声明视图层.

2.`简单的更新流程`,只需要定义UI状态,React便会负责把它渲染成最终的UI.

3.`灵活的渲染实现`,React先把他们渲染成虚拟的DOM,虚拟DOM只是普通的JavaScript对象,结合其他依赖库把这个对象渲染成不同终端上的UI.

4.`高效的DOM操作`,尽量减少虚拟DOM到真实DOM的渲染次数,以及每次渲染需要改变的真实DOM节点数.

*React总的来说,关注的是如何根据状态创建可复用的UI组件*

## 开发环境
 
### 基础环境
 
 1.[Node.js][nodejs] 
 
 *在服务器端运行的JavaScript.*
 
 2.NPM  
 *模块管理工具,用来管理模块的发布,下载及模块之间的依赖关系.*(安装好nodejs,npm也自动装好了)
 
 
### 辅助工具
 
####  1.[webpack][webpack]
 
 *现代JavaScript应用程序的模块打包工具*
 
####  2.Babel
 
 *JavaScript编译器,它可以将ES6及其以后的语法编译成ES5的语法*

#### 3.ESLint
 
 *插件化的JavaScript代码检测工具* 
 
 **Create React App**  [React-cli][creatreactapp]
 
 1.安装
 ```
    npm install -g create-react-app
 ```
 *通过使用-g参数,安装到系统的全局环境,这样就可以在任意路径下使用它.*
 
 2.创建应用
 ``` 
 create-react-app [appNmae]
 ```
 *在当前路径下新建一个名为[appName]的文件夹,[appName]就是新创建的React应用*
 
 3.运行应用
 ``` 
 cd [appName]
 
 npm start
 ```
 目录结构
``` 
 [appName]
 ├── node_modules  //安装的所有依赖模块;
 ├── package.json  //定义了项目的基本信息,如项目名称,版本号,在该项目下可执行的命令以及项目的依赖模块等;
 ├── public        //index.html是应用的入口页面;
 ├── src           //项目源代码,index.js是代码入口;
 └── yarn.lock
```
 
 
 
 
 
 
 
 
 
 [nodejs]: https://www.google.com/ "Nodejs"
 [webpack]: https://www.webpackjs.com/ "Webpackjs"
 [creatreactapp]: https://github.com/facebookincubator/create-react-app/ "react-cli"
 [react]: https://reactjs.org/ "React"
 [react2]: https://react.docschina.org/ "React"