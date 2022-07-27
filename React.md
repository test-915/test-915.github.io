```
https://www.youtube.com/watch?v=DbDzHLIUiQk&list=PLmOn9nNkQxJFJXLvkNsGsoCUxJLqyLGxu&index=64

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

