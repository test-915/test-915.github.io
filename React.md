```
https://www.youtube.com/watch?v=ssLYXXStf-Q&list=PLmOn9nNkQxJFJXLvkNsGsoCUxJLqyLGxu&index=110

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
import {Link， BrowserRouter} from 'react-router-dom'
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



## NavLink

```jsx
//实现link高亮效果,点击后class会带active属性
import {NavLink} from 'react-router-dom'
<NavLink classNmae='' to='/index'>首页</NavLink>

//实现点击后追加class属性
<NavLink activeClassName="active" classNmae='' to='/index'>首页</NavLink>
```



### 封装NavLink

```jsx
//创建组件MyNavLink
import {NavLink} from 'react-router-dom'
render (){
	return (
		<NavLink {...this.props} />
	)
}

//引入组件到App
<MyNavLink to="/index" a={a} b={b} c={c} >首页</MyNavLink>
```



## Switch

```jsx
//不渲染同一个路由的多个路径
<Switch>
    <Route path="/home" component={Home1} />
    <Route path="/home" component={Home2} />
</Switch>
```



## 匹配模式

```jsx
//模糊匹配
<Route path="/home" component={Home1} />

//精准匹配
<Route exact={true} path="/home" component={Home1} />
<Route exact path="/home" component={Home1} />
```



## 默认路由

```jsx
import {Redirect} from 'react-router-dom'

<Switch>
    <Route path='home' component={home} />
    <Route path='home2' component={home2} />
	<Redirect to='/home' />
</Switch>
```



## 路由传参



### params传参

> this.props.match.params

```jsx
//传参
<Link to={`/detail/${id}`}>链接</Link>

//声明接收
<Route path="/detail/:id" component={Detail} />

//组件接收
const data = [
    {id:'1',content:'正文'}
]
const {id} = this.props.match.params
connst findResult = data.find((obj) => {
    return obj.id === id	//数据id等于查询的id，则返回数据对象
})
```



### search传参

> this.props.location.search

```jsx
//传参
<Link to={`/detail/?id=${id}`}>链接</Link>

//正常注册路由
<Route path="/detail" component={Detail} />

/*引入querystring  qs讲urlencode 转 对象*/
import qs from 'querystring'

//组件接收
const {search} = this.props.location
const {id} = qs.parse(search.slice(1) )
connst findResult = data.find((obj) => {
    return obj.id === id	//数据id等于查询的id，则返回数据对象
})
```



### state传参

> this.props.location.state

```jsx
//传入对象给组件
<Link to={{pathname:'/index', state:{id:obj.id} }}>链接</Link>
    
//正常注册路由
<Route path="/detail" component={Detail} />

//组件接受
const {id} = this.props.location.state
connst findResult = data.find((obj) => {
    return obj.id === id	//数据id等于查询的id，则返回数据对象
})
```



## 路由跳转

> history有2种操作类型，PUST和REPLCE，路由跳转默认为PUSH，

```jsx
//开启replace跳转
<Link replace={true} to={`/detail`}>链接</Link>
```



## 编程式路由导航



### 跳转方法

> 配合使用对应的传参模式params/search/state

```jsx
//replace跳转
replaceShow = (id)=>{
    this.props.history.replace(`/detail/${id}`)
}
<button onClick={ ()=>this.replaceShow(id) }>跳转</button>

//push跳转
pushShow = (id)=>{
    this.props.history.push(`/detail/${id}`)
}
<button onClick={ ()=>this.pushShow(id) }>跳转</button>

//state传参方法
replaceShow = (id)=>{
    this.props.history.replace(`/detail`, {id}) //传入路径和state对象
}
<button onClick={ ()=>this.replaceShow(id) }>跳转</button>
```



### 前进后退

```jsx
//前进
() => {
	this.props.history.goForward()
}

//后退
() => {
	this.props.history.goBack()
}

//前进或后退n步，负数为后退
(n) => {
    this.props.history.go(n)
}
```



## 一般组件使用路由组件

```jsx
//给一般组件引入withRouter
import {withRouter} from 'react-router-dom'

class Header extends Component {	
}

//暴露withRouter返回的组件
export default withRouter(Header)
```





# UI组件库

> 国外用material-ui
>
> 国内用蚂蚁金服的ant-design
>
> 饿了吗UI：element ui
>
> 有赞UI：vant 针对移动端



## 安装

```
yarn add antd
```



## 引入样式

```jsx
import 'antd/dist/antd.css'
```



## 按需引入

> 按需引入需要先执行，修改配置文件流程



### 安装

```
$ yarn add craco-less
```



### 修改配置

```jsx
/*craco.config.js*/
const CracoLessPlugin = require('craco-less');

module.exports = {
  plugins: [
    { /*以下配置修改primary-color*/
      plugin: CracoLessPlugin,
      options: {
        lessLoaderOptions: {
          lessOptions: {
            modifyVars: { '@primary-color': '#1DA57A' },
            javascriptEnabled: true,
          },
        },
      },
    },
  ],
};
```



# 修改配置文件

> 用不显示webpack隐藏文件的方式修改配置文件



### 安装

```
$ yarn add @craco/craco
```



### 修改

```json
/* package.json */
"scripts": {
    /*删除*/
-   "start": "react-scripts start",
-   "build": "react-scripts build",
-   "test": "react-scripts test",
    /*新增*/
+   "start": "craco start",
+   "build": "craco build",
+   "test": "craco test",
}
```



### 创建

```js
/* craco.config.js */
module.exports = {
  // ...
};
```



# Redux

> 组件间通信
>
> 集中式状态管理



## 安装

```
yarn add redux
```



## Shore

> shore.js专门用于暴露一个shore对象，整个应用只有一个shore对象

```jsx
// src/redux/store.js
//引入createStore
import {createStore} from 'redux'
//引入为shore服务的reducer功能文件
//例如处理count的reducer命名为countReducer
import {countReducer} from './count_reducer'

export default createStore(countReducer)
```



## Reducer

> Reducer本质是函数

```jsx
/* 创建用于处理count的count_reducer.js文件 */
const initState = 0 //初始化赋值方法1 
export default function countReducer(preState=initState, action){ //传入之前的状态 和 动作对象
    /* 初始化方法2
    if(preState == undefined) preState = 0 // 初始化赋值
    */
	const {type, data} = action
    // 根据type决定如何加工数据
    switch (type){
        case 'increment':
            return preState + data
        case 'decrement':
            return preState - data
        default: //返回初始化值
            return preState
    }
}
```



## 获取状态

```jsx
//组件中引入store
return (
    <div>
    	{store.getState()} //从shore获取状态
    </div>
)
```



## 创建action对象

```jsx
shore.dispatch({type:'increment', data:value })
//value将进行increment类型的加工
```



## 检测状态



### 组件内检测

```jsx
componentDidMount(){
	//检测redux状态变化，只要变化就调用render
	store.subscribe(()=>{
		this.setState({})
	})
}
```



### 全局检测

```jsx
/* index.js */
import store from './redux/store'

//redux发生变化，渲染整个app
store.subscribe(()=>{
    ReactDom.render(
        <App/>,
        document.getElementById('root')
    )
})
```



## Action对象



### 同步action

```jsx
/* 处理count的action对象，创建count_action.js文件 */

// 处理Increment方法的action对象
export const createIncrementAction = data => ({type:'increment', data})
```



### 异步action

> 依赖中间件
>
> 安装：yarn add redux-thunk

```jsx
export const createIncrementAsyncAction = (data, time) => {
    //返回一个函数给shore，shore会调用这个函数并传入dispatch
	return (dispatch)=> {
		setTimeout( ()={ 
            //时间一到，触发dispatch，传入action的一般对象
			dispatch(createIncrementAction(data))
		},time)
	}
}
```

```jsx
/* store.js */
/*  引入thunk */
import thunk from 'redux-thunk'
/* 引入中间件 */
import {applyMiddleware} from 'redux'

//暴露shore时，应用中间件
export default  createStore(countReducer, applyMiddleware(thunk) )

```





# React-Redux



## 安装

> yarn add react-redux



## 容器



### 完整容器

```jsx
/* 创建名为Count的容器组件containers/Count/index.jsx */
//引入名为Count的UI组件
import CountUI from '../../components/Count'
//引入connect用于连接UI组件与redux
import {connect} from 'react-redux'
//引入名为Increment的aciton对象
import {createIncrementAction} from '../../redux/count_action'

/*
mapStateToprops返回给UI组件的状态，
容器组件会自动调用shore获取state 并传递给a函数
*/
const mapStateToprops = (state)=>{
    //返回的对象类似于props，key作为UI组件的状态属性名，val作为UI组件的状态属性值
    return {key:state}
}

/*
b返回操作状态的方法,自动调用shore获取dispatch
*/
const mapDispatchToprops = (dispatch)=>{
    return {
        //创建一个jia的方法
        jia:(data)=>{//传入dispatch需要的数据
            //通知redux执行加法
            dispatch(createIncrementAction(data))
        }
    }
}

//获取名为Count的容器组件,传入props
export default connect( mapStateToprops,mapDispatchToprops )(CountUI)
```



### 容器代码简化

```jsx
/* 创建名为Count的容器组件containers/Count/index.jsx */
//引入名为Count的UI组件
import CountUI from '../../components/Count'
//引入connect用于连接UI组件与redux
import {connect} from 'react-redux'
//引入名为Increment的aciton对象
import {createIncrementAction} from '../../redux/count_action'


//获取名为Count的容器组件,传入props
export default connect( 
    state => ({key:state}),
    dispatch => (
        jia:(data)=> dispatch(createIncrementAction(data))
	)
)(CountUI)
```



### API容器简化

```jsx
/* 创建名为Count的容器组件containers/Count/index.jsx */
//引入名为Count的UI组件
import CountUI from '../../components/Count'
//引入connect用于连接UI组件与redux
import {connect} from 'react-redux'
//引入名为Increment的aciton对象
import {createIncrementAction} from '../../redux/count_action'


//获取名为Count的容器组件,传入props
export default connect( 
    state => ({key:state}),
    /*
    	直接传入对象，value不调用函数，直接用函数赋值，
    	react-redux会自动调用dispatch传入value执行
    */
    {
        jia:createIncrementAction
	}
)(CountUI)
```



## 使用容器

```jsx
/* 在上级组件传入容器组件 */
import store from './redux/store'

export default class App extends Component {
	render() {
        return (
            <div>
            	<Count store={store} />
            </div>
        )
    }
}
```



## 一次性传递store

```jsx
import {Provider} from 'react-redux'
//Provider将store传递给app里面的所有容器
ReactDOM.render(
	<Provider store={store}>
		<App/>
	</Provider>,
    document.getElementById('root')
)
```



## 检测状态

> 使用react-redux不需要再通过store.subscribe检测状态，connect已经实现检测



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

