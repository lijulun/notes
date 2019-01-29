# JSX语法
[官网](https://jsx.github.io/ 'jsx')  [中文](https://www.tslang.cn/docs/handbook/jsx.html '中文')
### 基础概要
* JSX语法
* 组件的概念及使用
* 列表渲染
* 事件处理
* 表单

### JSX简介

JSX是一种用于描述UI的JavaScript扩展语法,React使用这种语法描述组件的UI.

### JSX语法

#####  基本语法

JSX的基本语法和XML语法相同,都是使用成对的标签构成树状结构的数据.
``` 
const element = (
    <div>
        <h1>Hello,world!</h1>
    </div>
)  
```
#####  标签类型

两种标签类型
* DOM类型的标签(div,span等)
* React组件类型的标签

使用规则定义
* DOM:标签的首字母必须要小写.
* React:标签的首字必须要大写.

*React 正是通过首字母的大小写判断渲染的是一个DOM类型的标签还是一个React组件的标签*
``` 
//DOM类型标签
const element = <h1>Hello,world!</h1>

//React 组件类型标签
const element = (
    <div>
        <HelloWorld /> //注意反斜线收尾
    </div>
)

//两者可以混合使用
```
##### 3 JavaScript 表达式

JSX可以使用JavaScript表达式,因为JSX本质上仍然是JavaScript.在JSX中使用表达式必须使用大括号"{}"包起来.

``` 
//通过表达式给标签属性赋值
const element = <MyComponent foo = {1 + 2} />

//通过表达式定义组件(map 虽然是函数,但它的返回值是JavaScript表达式)
const todos = ['item1','item2','item3']
const element = (
    <ul>
        {todos.map(message => <Item key={message} message = {message} />)}
    </ul>
)
```
* JSX中只能使用JavaScript表达式,而不能使用多行JavaScript语句.
* 可以使用三元运算符或逻辑与(&&)来代替if语句

##### 4 标签属性

当JSX标签是DOM类型的标签时,对应的DOM标签支持的属性JSX也支持.例如id,class,style,onclick,但是
部分属性的名称所有变化;
* class > className
* 事件的属性名采用驼峰格式,例如 onclick采用onClick
``` 
//DOM标签属性
<div id = 'content' className = 'foo' onClick = {()=>{console.log('hello,world!')}}></div>
//React标签属性
<User name = 'React' age = '4' address = 'America' />
```

##### 5 注释

JSX 中的注释需要使用大括号"{}" 将/**/包裹起来.
``` 
const element = (
    <div>
        {/*这里是注释*/}
    </div>
)
```

##### 6 JSX不是必须的

JSX语法对使用React来说不是必须的,实际上JSX语法只是React.createElement(component,props,...children)的语法糖,所有的JSX最终都会转换成对这个方法的调用. 

``` 
//JSX语法
const element = <div className = 'foo'> Hello,world!</div>

//转换后
const element = React.createElement('div',{className:'foo'},'Hello,world');
```
##### 7 最外层必须要唯一div标签包裹或者使用React.Fragment


### 组件

组件是React的核心概念,是React应用程序的基石.组件将应用的UI拆分成独立的,可复用的模块,React应用程序正是由一个一个组件搭建而成.

##### 1 定义组件

两种方式

+ ES 6 class(类组件)
    + 1 class 继承自React.Component
    + 2 class 内部必须定义render方法,render方法返回代表该组件的UI的React元素
``` 
自定义组件
//PostList.js
import React,{ Component } from "react";
class PostList extends Component {
    render(){
        return (
            <div>
                帖子列表
                <ul>
                    <li>内容</li>
                    <li>内容</li>
                    <li>内容</li>
                    <li>内容</li>
                    <li>内容</li>
                    <li>内容</li>
                </ul>
            </div>
        );
    }
}

export default PostList;
```
    在定义组件后,使用ES 6 export 将PostList作为默认模块导出,从而可以在其他JS文件中导入PostList使用.
``` 
//挂载到DOM节点
import React from "react";
import ReactDom from "react-dom";
import PostList from "./PostList";

ReactDom.render(<PostList />,document.getElementById("root"));
```
+ 使用函数(函数组件)
``` 
function Welcome(props){
    return <h1>hello,{props.name}</h1>
}
```


##### 2 组件的props

组件的props用于把父组件中的数据或方法传递给子组件,供子组件使用.
props是一个简单结构的对象,它包含的属性正是由组件作为JSX标签使用时的属性组成.
```
//User 组件 
<User name = 'React' age = '4' address = 'America' />

//此时User组件的props结构如下:
props = {
    name : 'React',
    age : '4',
    address : 'America'
}

//使用props定义组件

import React,{ Component } from "react";

class PostList extends Component {
    render(){
        const { title,age,date } = this.props;
        return (
            <li>
                <div>{title}</div>
                <div>{age}</div>
                <div>{date}</div>
            </li>
        );
    }
}

export default PostList;

```

**3 组件的state**

组件的state是组件内部的状态,state的变化最终将反映到组件UI的变化上.

定义:在构造方法constructor中通过this.state定义初始状态
修改:通过调用this.setState方法改变组件状态(唯一方式)

``` 
import React,{ Component } from "react";

class PostList extends Component {
    constructor(props) {
        super(props); //完成React组件的初始化工作
        this.state = {
            vote : 0
        }
    }

    render(){
        const { title,age,date } = this.props;
        return (
            <li>
                <div>{title}</div>
                <div>{age}</div>
                <div>{date}</div>
                <button onClick = {
                        ()=>{
                            this.handleClick();
                            }
                        }>
                    点赞
                </button>
                <span>{this.state.vote}</span>
            </li>
        );
    }
}

export default PostList;
```
*React 组件正是由props和state两种类型的数据驱动渲染出组件UI*

*props是组件对外的接口,组件通过props接收外部传入的数据(包括方法);*

*state 是组件对内的接口,组件内部状态的变化都是通过state来反映的;*

** 有状态组件和无状态组件 **

* 有状态组件:一个组件的内部状态会发生变化,就需要使用state来保存变化
* 无状态组件:一个组件的内部状态是不变的,就用不到state,在使用无状态组件时,应该尽量将其定义成函数组件.

##### 4 属性效验和默认属性
* 组件调用属性效验时需要注意的地方
    + 组件.propTypes(首字母小写)
    + 属性.PropTypes(首字母大写)

React提供了PropTypes这个对象,用于效验组件属性的类型.
``` 
PostList.PropTypes = {
    post : PropTypes.object,
    onVote : PropTypes.func
}
```
| 类型 | PropTypes对应属性 |
| :------:| :------: |
| String | PropTypes.string |
| Number | PropTypes.number |
| Boolean | PropTypes.bool |
| Function | PropTypes.fun |
| Object | PropTypes.object |
| Array | PropTypes.array |
| Symbol | PropTypes.symbol |
| Element | PropTypes.element |
| Node(可被渲染的节点:数字,字符串,React元素或由这些类型的数据组成的数组) | PropTypes.node |

*复合数据如何效验(object,array)*

PropTypes.shape或者PropTypes.arrayOf
``` 
//对象
style:PropTypes.shape({
    color:PropTypes.string,
    fontSize:PropTypes.number
}),

//数组
sequence:PropTypes.arrayOf(PropTypes.number);
```
*必须属性*

在PropTypes的类型属性上调用isRequired
``` 
    PostList.propTypes = {
        post:PropTypes.shape({
            id:PropTypes.number,
            title:PropTypes.string
        }).isRequired
    }
```
*默认属性*
``` 
function Welcome(props){
    return <h1 className="foo">Hello,{props.name}</h1>
}

Welcome.defaultProps = {
    name:'Stranger'
}
```

##### 5 组件的样式

两种方式添加样式
* 外部css样式

这种方式和我们平时开发Web应用时使用外部CSS文件相同,唯一的区别是class换成className

``` 
//无状态组价
function Welcome(props){
    return <h1 className = 'foo'>Hello,{props.name}<h1>
}

//style.css
.foo{
    width:100%;
    height:50px;
}

//通过组件的的HMTL标签引入
<link rel="stylesheet" type="text/css" href="style.css">

//以模块的形式引入
import './style.css';
```
补充说明:使用css样式表经常遇到class名称冲突,业内解决这个问题的常用方案是使用CSS Modules
[github](https://github.com/css-modules/css-modules)

* 内联样式
``` 
function Welcome(props){
    return (
        <h1 
        style = {{
            width:"100%",
            height:"100%",
        }}>
        Hellow,{props.name}
        </h1>
    );
}
```
* 使用内联样式需要注意:
    + 样式的属性名必须使用驼峰格式的命名,backgroudcolor > backgroudColor