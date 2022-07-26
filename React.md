```
https://www.youtube.com/watch?v=vU3MVB5IxUY&list=PLmOn9nNkQxJFJXLvkNsGsoCUxJLqyLGxu&index=35
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



## 旧版的生命周期



### 挂载时

> 1.constructo //构造器
>
> 2.componentWillMount //将要挂载
>
> 3.render 渲染组件
>
> 4.componentDidMount //完成挂载后
>
> 5.componentWillUnmount //卸载



### 更新时



#### setStatic更新

> 2.shouldComponentUpdate //是否应该更新，默认为true
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后
>
> 6.可能卸载



#### forceUpdate强制更新

> 不修改状态
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后
>
> 6.可能卸载



#### 父组件render

> 2.shouldComponentUpdate //是否应该更新，默认为true
>
> 3.componentWillUpdate //将更新
>
> 4.render //渲染
>
> 5.componenDidUpdate //更新后
>
> 6.可能卸载



##### 如何挂载父子组件

```jsx
render(){
	return(
		<div>
			<B/> //子组件类名
		</div>
	)
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

