```
https://www.youtube.com/watch?v=rmoSGnyE8sY&list=PLmOn9nNkQxJEARHuEpVayY6ppiNlkvrnb&index=20
```



# 配置



## 配置生产提示

```js
//阻止vue的环境提示
Vue.config.productionTip = false 
```



## 定制键盘别名

```js
Vue.config.keyCodes.huiche = 13
```





# 绑定容器



## 通过对象绑定

```js
new Vue({
	el:'#root',
	data:{
	}
})
```



## 通过实例绑定

```js
coust v = new Vue({})
v.$mount('#root')
```



# 数据



## 对象式数据

```js
//可能会报错
new Vue({
	el:'#root',
	data:{
		//数据
	}
})
```



## 函数式数据

```js
new Vue({
	el:'#root',
	data:function(){ //不能写箭头函数，因为箭头函数会向外找this
		return {}//数据
	}
})
//简写
new Vue({
	el:'#root',
	data(){ //不能写箭头函数，因为箭头函数会向外找this，this不再是vue实例
		return {}//数据
	}
})
```



# 插入数据



## 属性插值实现

```js
new Vue({
    data:{

    }
})
```



## methods实现

> 没有缓存，调用几次就计算几次

```js
new Vue({
    methods:{

    }
})
```





## 计算属性实现

> 有缓存，每次改变依赖数据时，只会调用一次，然后用缓存复用

```js
new Vue({
    computed:{
		fullName:{
            get(){//给这个对象创造一个get方法来绑定一个数值，当前this指向vm
                return this.num1 + this.num2
            },
            set(){...}//当fullName被修改时，将会执行这个方法
        }
        fullName(){...}//简写,只需要get，不需要set时可以直接把get方法给fullName
    }
})

```





# 数据绑定



## 单向绑定

```vue
<div v-bind:id=id ></div>
简写：
<div :id=id ></div>
```



## 双向绑定

```vue
只能用于表单类元素
<div v-model:id=id ></div>
简写
<div v-model=id ></div>
```



# 数据代理



## object数据代理

```js
let person = {}
//以下方法不可枚举，不可修改，不可删除
Object.defineProperty(person, 'age', {
	value:18
})
//如何实现枚举/修改/删除？
Object.defineProperty(person, 'age', {
	value:18,
    enumerable:true,//控制属性是否枚举，默认为false
    writable:true,//控制属性是否可修改
    configurable:true//控制属性是否可删除
})

//给对象绑定一个变量，数据可以现用现取
let person = {}
let number = 18
Object.defineProperty(person, 'age', {
    //有人读取age的时候，会返回最新的number值
    get(){
        return number 
    },
    //有人修改set值，会调用set方法，set会受到修改值
    set(value){
		number = value //把number值改成value值
    }
})
```



# 点击事件



## vue方法

```html
//创建
//v-on可以绑定一个vue方法
<button v-on:click="showInfo">点击</button>
//简写
<button @click="showInfo">点击</button>

//传参同时传入event,不传evnet则不要加$event占位符
<button @click="showInfo2(99,$event)">点击</button>

<script>
//创建实例
new Vue({
    el:'#root',
    data:{},
    methods:{
        //不传参方法
        showInfo(event){ //创建了一个名为showInfo的方法，回调传入事件对象
            alert('')//这个地方的this是vm
        },
        //传参方法,如果要传参
        showInfo2(number,event){
        },
    }
})
</script>
```



# 事件修饰符



## 阻止默认跳转事件

```html
<a href="" @click.prevent="showInfo">点击不跳转</a>
```



## 阻止事件冒泡

```html
<button @click.stop="showInfo">点击</button>
```



## 只触发一次事件

```html
<button @click.once="showInfo">点击</button>
```



## 捕获模式

```html
<button @click.capture="showInfo">点击</button>
```



## 只有e.target是当前元素才会触发

```html
<button @click.self="showInfo">点击</button>
```



## 不等待事件回调

```html
wheel是滚动触发事件，加了passive后不再等待showInfo事件，直接执行滚动
移动端可能会用
<ul @wheel.passive="showInfo">
    <li>1</li>
    <li>2</li>
    <li>3</li>
</ul>
```



### 组合修饰符

```html
<a href="" @click.stop.prevent="showInfo">点击不跳转</a>
```





# 键盘事件



## 按键别名



> enter/delete/esc
>
> space/tab
>
> up/down/left/right



## 绑定键盘

```html
松开退格或者删除时，触发
<input @keyup.delete="showInfor" />
```



## 组合绑定

```html
同时按下ctrl+y才会触发
<input @keyup.ctrl.y="showInfor" />
```

