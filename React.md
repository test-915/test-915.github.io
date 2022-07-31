```
https://www.youtube.com/watch?v=IQhzYuw1ZvQ&list=PLmOn9nNkQxJFJXLvkNsGsoCUxJLqyLGxu&index=78

未完成
```





# 组件三大属性





## 状态：state





### 初始化状态

```
state = {
	key: ''
}
```





### 修改状态

```jsx
this.setState({key:val})
```





## 定位：refs





## 传参：props





# 收集表单数据





## 受控与非受控组件

> 随着输入的数据改变状态，提交数据时从状态中获取数据，就是受控组件。
>
> 现用现取，就非受控组件。





## 获取事件源

```js
dome = (event)=>{
	console.log(event.target) //event为事件源
}
```



### 获取事件键盘编码

```js
event.keyCode
```







## 阻止表单提交

```jsx
handleSubmit = (event)=>{
	event.preventDefault()
}
```





## form表单提交事件
```jsx
<form onSubmit={this.handleSubmit}>
</form>
```





## 设置回调函数ref

```jsx
<input ref={c => this.username = c} />
```





## 获取回调函数ref

```jsx
handleSubmit = ()=>{
	const {username} = this
}
```





# 组件生命周期





## 组件挂载

```jsx
ReactDOM.render(
    <Dome/>, //组件类名
    document.getElementById('test')
)
```





## 组件卸载

```jsx
ReactDome.unmountComponentAtNode( document.getElementById(test'') )
```





## 渲染函数

```jsx
class Dome extends React.Component{
    //初始化渲染和状态更新后调用render
    render(){
		return(
            <div></div>
		)
    }
}
```





## 挂载时调用函数

```jsx
componentDidMount(){
	//挂载后/初始化渲染后调用一次
}
```





## 组件将要卸载调用函数

```jsx
componentWillUnmount(){
	//卸载前执行的
}
```





## v16生命周期





### 挂载组件

> 1.constructo //构造器
>
> 2.componentWillMount //将要挂载
>
> 3.render 渲染组件
>
> 4.componentDidMount //完成挂载后





### 更新组件

> 更新后函数componenDidUpdate，接受preProps, preStatic, snapshotValue，也就是先前的值，和快照值。



#### setStatic更新

> 2.shouldComponentUpdate //是否应该更新，默认为true
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后





#### forceUpdate强制更新

> 不修改状态
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后





#### 父组件render

> 1.componentWillReceiveProps //子组件接受父组件传递过来的参数
>
> 2.shouldComponentUpdate //是否应该更新，默认为true
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后





##### 组件将要接受新的props钩子

```
componentWillReceiveProps(props){
	//组件将要接受新的props钩子
}
```





##### 如何挂载父子组件

```jsx
//A组件
static = {carName:'奔驰'}
render(){
	return(
		<div>
			<B carName={this.state.carName} /> //子组件类名
		</div>
	)
}
//B组件
render(){
	return(
		<div>B组件{this.props.carName}</div>
	)
}
```





### 卸载组件

```jsx
//触发器
ReactDom.unmountComponentAtNode()
//触发函数
componentWillUnmount()
```





## v17生命周期





### 不推荐的钩子

> componentWillMount 
>
> componentWillReceiveProps 
>
> componentWillUpdate 
>
> 以上钩子需要加上UNSAFE_作为前缀





### 让状态取决参数

> 功能：从props传递给static状态，让static状态在任何时候都取决于props
>
> 挂载时作用于，构造器之后。
>
> 更新时作用于，render和shouldComponentUpdate之前。
>
> 1.必须静态

```jsx
static getDerivedStateFromProps(props, static){
	return {} //返回状态对象
}
```





### 生成快照

> getSnapshotBeforeUpdate(prevProps, prevStatic){
>
> ​	return snapshotValue //快照值，任何类型
>
> }
>
> 传递给componentDidUpdate的快照值snapshotValue
>
> componentDidUpdate(prevProps, prevStatic, snapshotValue)





# 脚手架



## 安装包

```
npm install -g create-react-app
//或者
npm i create-react-app -g
```





## 创建项目

```
create-react-app app_name
```





## 脚手架命令

```
//开启开发者服务器
npm start 
yarn start

//打包项目
npm run build
yarn build

//测试库
npm test
yarn test

//显示webpack.config
npm run eject
yarn eject
```





## 创建并暴露App组件

```jsx
// App.js
import React,{Component} from 'react'
export default class App extends Component{
  render(){
    return (
      <div>
        hello
      </div>
    )
  }
}
```



## 样式模块化

```jsx
//样式文件名：style.module.css
//引入样式
import style from 'style.module.css'
//使用样式
<div className={sytle.class-name} ><div>
```



## 代码提示

> 安装插件es7 react/redux/graphQL





## 组件创建流程

> 1.拆分组件
>
> 2.实现静态组件
>
> 3.实现动态组件
>
> ​	a.





## UUID

```jsx
//uuid大库
npm i uuid
//uuid小库
yarn nanoid
//使用
import {nanoid} from 'nanoid'
console.log(nanoid())
```



## PropTypes

> //安装
>
> yarn add prop-types
>
> //引入
>
> import PropTypes from 'prop-types'



## 类型约束

```
static propTypes = {
	key: PropTypes.func.isRequred, //key函数为必选值
	key1: PropTypes.array.isRequred, //key1数组为必选值
}
```





# axios



## 安装

> yarn add axios



## 发送请求

```jsx
axios.get('').then(
	response => {
		//响应数据:reponse.data;
	},
	error => {
		//错误信息:error
	}
)
```



## 代理转发



### 单个代理

```json
//package.json添加代理
{
    "proxy":"http://localhost:5000"
}
```



### 多个代理

```js
//创建文件src/setupProxy.js
const proxy = require('http-proxy-middleware')
module.exports = function(app){
    app.use(
    	proxy('/api1',{  //匹配路径
            target:'http://localhost:5000', //转发给谁
            changeOrigin:true,  //控制服务器收到的请求头HOST值
            pathRewrite:{'^/api1':''} //重写请求路径，替换掉api1路径字串
        })
    )
}
```



# fetch



```
fetch(url).then(
	response => {
		return response.json()
	}, //联系服务器成功
).then(
	response => {},
	error => {}
).catch(
	(error) => {}
)
```



```
fetch(url).then(
	response => {
		return response.json()
	}, //联系服务器成功
).then(
	response => {},
	error => {}
).catch(
	(error) => {}
)
```



# 消息订阅



## 安装PubSubJS

```
npm install  pubsub-js --save
yarn add pubsub-js
```



## 引入

```jsx
import PubSub from 'pubsub-js'
```



## 订阅

```jsx
token = PubSub.subscribe('name', function(msg, data){} )
token = PubSub.subscribe('name', (msg, data) => {} )
```



## 发布消息

```jsx
PubSub.publish('name',data)
```



## 取消订阅

```jsx
PubSub.unsubscribe(this.token )
```



# 路由



## 安装路由器

> npm i react-router-dom



## link

```jsx
//引入
//BrowserRouter为h5路由
//HashRouter为锚点路由
import {link， BrowserRouter} from 'react-router-dom'
import Index from ‘./components/Index’


<BrowserRouter>
	//创建链接
	<Link classNmae='' to='/index'>首页</Link>
	//注册路由
	<Route path='/index' component={Index}/>
</BrowserRouter>
```



## 路由装到index

```jsx
import {BrowserRouter} from 'react-router-dom'

//index.js
//不用在安装到组件内
ReactDOM.render(
	<BrowserRouter>
        </App>
	</BrowserRouter>,
	document.getElementById('root')
)
```





# js语法





## 箭头函数

```js
demo = ()=>{
	//函数体
}
```





## 变量对象名

```jsx
key = 'key_name'
obj = {[key]:val}
//等价于
obj[key] = val
```





## 定时器

```jsx
this.timer = setInterval(
	() => {
		console.log('')
	},200
)
//卸载定时器
clearInterval(
	this.timer
)
```



## 数组条件统计

```
reduce
```

