```
https://www.youtube.com/watch?v=VN7G5be9t4U&list=PLmOn9nNkQxJEARHuEpVayY6ppiNlkvrnb&index=154

未完成
```



# 配置



## .配置生产提示

```js
//阻止vue的环境提示
Vue.config.productionTip = false 
```



## .定制键盘别名

```js
Vue.config.keyCodes.huiche = 13
```





# 绑定容器



## .通过对象绑定

```js
new Vue({
	el:'#root',
	data:{
	}
})
```



## .通过实例绑定

```js
coust v = new Vue({})
v.$mount('#root')
```



# 数据



## .对象式数据

```js
//可能会报错
new Vue({
	el:'#root',
	data:{
		//数据
	}
})
```



## .函数式数据

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



## .属性插值实现

```js
new Vue({
    data:{

    }
})
```



## .methods实现

> 没有缓存，调用几次就计算几次

```js
new Vue({
    methods:{

    }
})
```





## .计算属性实现

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



# 监视属性



## .通过对象监视

```js
const vm = new Vue({
    watch:{
        //可以监视对象属性，也可以监视计算属性computed
        isHot:{
            //再isHot发生改变时，调用handler，并传入新值和旧值
            handler(newValue, oldValue){
                
            }
            //是否初始化时调用，默认为false，不立刻执行
            immdiate:true,
        }
    }
})

//简写，只需要handler不需要其他属性的监视，可以简写
const vm = new Vue({
    watch:{
        isHot(newValue, oldValue){
        }
    }
})
```



## .通过实例监视

```js
coust vm = new Vue({})
vm.$watch('isHot',{
    handler(){}
})

//简写，只需要handler不需要其他属性的监视，可以简写
coust vm = new Vue({})
vm.$watch('isHot',function(newValue, oldValue){
    
})
```



## .深度监视

```js
const vm = new Vue({
    watch:{
        dic:{
            //是否开启深度监视，监视多级结构dic对象中的所有属性变化，
            //默认为false只监视dic本身而不监视多级结构中的对象内部。
            deep:true,
        }
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



### 双向绑定修饰符

```vue
//指定数据为数字
<div v-model.number=id ></div>
```



### 懒收集表单

```vue
//失去焦点再收集数据
<div v-model.lazy=id ></div>
```



### 去掉表单空格

```vue
//失去焦点再收集数据
<div v-model.trim=id ></div>
```



# 绑定样式



## 绑定class



### 字符串方式

> 场景：类名不确定，需要动态指定

```html
<div :class='mood' @click='changeMood'></div>

<script>
    new Vue({
        data:{
            mood:'normal'
        },
        methods:{
            changeMood(){
                //点击后，触发mood样式变更为happy
                this.mood = 'happy'
            }
        }
    })
</script>
```



### 数组方式

> 场景：样式个数不确定，名字不确定

```html
<div :class='mood' @click='changeMood'></div>

<script>
    new Vue({
        data:{
            mood:['c1', 'c2', 'c3']
        }
    })
</script>
```





### 对象方式

> 场景：样式个数不确定，名字不确定

```html
<div :class='mood' @click='changeMood'></div>

<script>
    new Vue({
        data:{
            mood:{
                c1:true, //true和false代表样式是否启用
                c2:false
            }
        }
    })
</script>
```



## 绑定style



### 字符串方式

```html
<div :style="{fontSize:fsize+'px'}" ></div>
```



### 对象方式

```html
<div :style="styleObj" ></div>

<script>
	new Vue({
        styleObj:{
            fontSize:40px
        }
    })
</script>
```



### 数组方式

```html
<div :style="[styleObj,styleObj2]" ></div>
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



# 条件渲染



## 隐藏

```html
v-show接受表达式，为true显示，为false隐藏
<div v-show='isShow'></div>
<div v-show='1 === 1'></div>

<script>
	new Vue({
        data:{
            isShow:false
        }
    })
</script>
```



## 不加载

```html
v-if，为true加载，为false不加载
if和else 不能打断，要紧挨着
<div v-if='isLoad'></div>
<div v-else-if='1 === number'></div>
<div v-else-if='2 === number'></div>
<div v-else=''>else不需要条件</div>

只做判断，不添加节点
<template v-if='isLoad'>
    不显示template节点
</template>

<script>
	new Vue({
        data:{
            isLoad:false
        }
    })
</script>
```



# 列表渲染



## 遍历数组

```html
<ul>
    <li v-for="p in persons" :key="p.id">
    	{{p.name}}
    </li>
    带index的遍历
    <li v-for="(p,index) in persons" :key="index">
    	{{p.name}}
    </li>
</ul>
```





## 遍历对象

```html
<ul>
    <li v-for="(value, key) in persons" :key="p.key">
    	{{value}}
    </li>
</ul>
```



## 遍历次数



```html
<ul>
    <li v-for="(number, index) in 5" :key="p.index">
    	{{number}}
    </li>
</ul>


```







## 列表过滤





### 监视属性实现

```html
<script>
	new Vue({
        data:{
            keyWord:'',
            persons:['','',''],
            filPersons:[]
        },
        watch:{
            keyWord:{
                immediate:true,
            	headler(val){
                    this.filPersons = this.persons.filter((p)=>{
                        return p.name.indexOf(val) !== -1
                    }
                }
            }
        }
    })
</script>
```



### 计算属性实现

```html
<script>
	new Vue({
        data:{
            keyWord:'',
            persons:['','',''],
            filPersons:[]
        },
        computed:{
            filPersons(){
                return this.persons.filter((p)=>{
                    return p.name.indexOf(this.keyWord) !== -1
                })
            }
        }
    })
</script>
```



## 列表排序

```html
<script>
	new Vue({
        data:{
            keyWord:'',
            persons:['','',''],
            filPersons:[],
            sortType:0,
        },
        computed:{
            filPersons(){
                const arr = this.persons.filter((p)=>{
                    return p.name.indexOf(this.keyWord) !== -1
                })
                if(this.sortType){
                    arr.sort((a,b)=>{
                        return this.sortType === 1 ? a.age-b.age : b.age-a.age
                    })
                }
                return arr
            }
        }
    })
</script>
```



# 追加属性

```js
//实例追加
Vue.set(vm.student,'sex','男') //再student属性中添加sex为男的属性
vm.$set(vm.student,'sex','男') //同理
vm.$delete(vm.student) //删除一个属性


//对象内部
const vm = new Vue({
    data:{student:{}},
    methods:{
        addSex(){
            this.$set(this.student,'sex','男')
        }
    }
})
```



# 过滤器



## 调用过滤器

```html
{{time | timeFormater}} 
timeFormater可以传参，将作为过滤器的第二个参数，第一个参数是管道符前的参数
```



## 配置过滤器

```js
new Vue({
	filters:{
		timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){
            return dayjs(value).format(str) //dayjs依赖三方库
        }
	}
})
```



## 全局过滤器

```
Vue.filter('mySlice',function(value){
	return value.slice(0,4)
})
```



# 内置指令



## 标签体文本

```
v-text
```



## 标签体结构文本

```
v-html
```



## 解析前样式

```html
<style>
    [v-cloak]{}
</style>
<div v-cloak></div>
v-cloak在解析页面后自动移除
```



## 读取1次

```html
<div v-once>{{n}}</div>
```



## 跳过解析

```html
<div v-pre="n">{{n}}</div>
```



# 自定义指令



## 简单方法

```html
<div v-big>
    
</div>
<script>
new Vue({
    directives:{
        big(element,binding){//传入真实dom，和一个binding绑定对象
            element.innerText = binding.value * 10 //原生js操作节点
            //实现效果value*10
        }
    }
})
</script>
```



## 完整方法

```html
<script>
new Vue({
    directives:{
        fbind:{
            //用简写的方式，相当于调用bind和update
        	//指定与元素绑定时(一上来)
        	bind(element,value){
        		element.value = binding.value
        	},
            //指令插入页面
        	inserted(element,value){
        		element.focus()
        	},
            //模板被重新解析时
            update(element,value){
                element.value = binding.value
            }
        }
    }
})
</script>
```



## 全局指令

```js
Vue.directive('fbind',{
	bind(){},
    inserted(){},
    update(){}
})
```



# 生命周期



## 挂载流程

```js
new Vue({
    beforeCreate(){},
    created(){},
	beforeMount(){},
	mounted(){},
})
```



## 更新流程

```js
new Vue({
    beforeUpdate(){},
    updated(){},
})
```





## 更新流程

```js
new Vue({
    beforeUpdate(){},
    updated(){},
})
```





## 销毁流程

```js
new Vue({
    beforeDestroy(){},
    destroy(){},
})
```





## 销毁实例

```js
vm.$destroy()
```



# 组件



## 创建组件

```js
const school = Vue.extend({
    name:'sbc',//自定义名称用于开发者工具
	data(){
        return {}
    }
})

//简写
const school = {
    name:'sbc',//自定义名称用于开发者工具
	data(){
        return {}
    }
}
```



## 注册组件

```js
new Vue(
	components:{
		xuexiao:school
	}
)
```



## 使用组件

```html
//组件标签：
<xuexiao></xuexiao>
```



## 嵌套组件

```
//父组件
const school = {
    name:'sbc',//自定义名称用于开发者工具
	data(){
        return {}
    },
    components:{
    	student//子组件
    }
}
```



# 单文件组件



## vue文件插件

> vetur 作者pine wu
>
> 快捷键：<v



## 编辑vue文件

```vue
//创建文件.vue
<timeplate>
</timeplate>

<script>
    export default {
        //组件体
        name:''
    }
</script>

<style>
</style>
```



# 脚手架



## 安装

> npm install -g @vue/cli



## 创建项目

> vue create appname



## 启动项目

> npm run serve



## 模板解析器

> 脚手架创建项目时，默认引入vue模块，module引入的模块残缺了模板解析器
>
> 造成main.js无法使用template
>
> 解决方法是指定引入完整版vue的路径，或者使用render

```js
//方法一：引入完整vue
import Vue from 'vue/dist/vue'

//方法二：render
new Vue({
    render(createElement){
        return createElement('h1', '标题')
    }
})
//简写
new Vue({
    render: h => h(App)
})
```



## 配置文件

> 创建文件vue.config.js
>
> 复写配置找官网



## Ref标签属性

```vue
配置ref
<div ref='abc'></div>

获取元素
this.$refs.abc
```



## 父子传参



### 父传子

```js
子组件声明接收参数
student = {
	//简单接收
	props:['name','age','sex']
	//条件约束接收
	props:{
		name:String,
		age:Number,
		sex:String
	},
	//复杂接收
	props:{
		name:{
			type:String,
			required:true//是否必须
		},
		name:{
			type:Number,
			default:99 //指定默认值
		},
	}
}

父组件传参数
<student name='n' :age='19' sex='m' >
:age值将作为表达式结果返回参数，返回数字19
age值将作为字符串，返回字符串19
```



### 子传父

> 父组件提前传递一个用于修改父组件状态的函数给子组件，子组件调用这个函数用于修改父组件



## 改参数

> props不允许修改，只能通过初始化给data传参，再修改data参数值

```
vc = {
	props:['name'],
	data(){
		return {
			name:this.name
		}
	}
}
```



## 混入



### 局部混入

```
// 定义混入对象
const myMixin = {
  created() {
    this.hello()
  },
  methods: {
    hello() {
      console.log('欢迎来到混入实例-RUNOOB!')
    }
  }
}
 
// 定义一个应用，使用混入
const app = Vue.createApp({
  mixins: [myMixin]
})
```



### 全局混入

```js
const app = Vue.createApp({
  myOption: 'hello!'
})
 
// 为自定义的选项 'myOption' 注入一个处理器。
Vue.mixin({
  created() {
    const myOption = this.$options.myOption
    if (myOption) {
      document.write(myOption)
    }
  }
})
```



## 插件

```js
//创建plugin.js
export default {
    install(Vue,a,b,c){
        //...插件任务
    }
}
    
//使用插件
import plugins from './plugins'
Vue.use(plugins,a,b,c)
```



## 样式作用域

```vue
<style scoped>
    /*样式作用限制在插件内*/
</style>
```



# 组件编码



## 流程

> 1.实现静态组件
>
> 2.转化为动态组件
>
> ​	2.1.数据的类型、名称是什么
>
> ​	2.2.数据要保存哪些组件
>
> 3.交互，绑定事件监听



## 条件输出属性

> 不知道标签是否需要属性，动态输出这个标签属性

```
<input type="checkbox" :checked="is_check" />

export default {
	data:{
		return {
			is_check:true
		}
	}
}
```



# 本地存储

> localStorage
>
> sessionStorage



## localStorage

```js
localStorage.setItem('key','val')
localStorage.getItem('key')
localStorage.removeItem('key')
localStorage.clearItem('key')//清空所有
```



## sessionStorage

> 浏览器一关就没了

```js
sessionStorage.setItem('key','val')
sessionStorage.getItem('key')
sessionStorage.removeItem('key')
sessionStorage.clear()//清空所有
```



# 自定义事件

> 实现父组件给子组件绑定自定义事件



## 原生事件

> 给组件绑定事件时，vue会把原生事件当成自定义事件，需要通过native修饰符声明

```
<Student @click.native='show'>
```



## v-on绑定

```
//父组件绑定事件
<Student v-on:test='demo'>//demo为父组件事件

//在子组件触发事件
export default {
	mothods:{
		sendStudent(){
			//触发方法
			this.$emit('test')
		}
	}
}
```



## ref绑定

```
//父组件传递事件给子组件：
export default{
	mouted(){
		//挂在后执行
		this.$refs.student.$on('refs标签',事件)
		//事件可以methods对象里的一个函数
		this.$refs.student.$on('refs标签',this.getSchoolName)
		//也可以是一个箭头函数，
		//但不能是普通函数，否则this将指向调用函数的那个组件
		this.$refs.student.$on('refs标签',(name,...params)=>{
			//...
		})
	}
}

//子组件的绑定与解绑参考v-on
```





## 解绑

```
//绑定事件
<Student v-on:test='demo'>//demo为父组件事件

export default {
	mothods:{
		unbind(){
			//解绑
			this.$off('test')
			//解绑多个
			this.$off(['test','test1'])
			//解绑全部事件
			this.$off()
		}
	}
}
```



# 全局事件总线



## 安装总线

```
//入口文件引入vue时配置全局事件
new Vue({
	//在创建组件前传递全局事件$bus到Vue原型里
	beforeCreate(){
		Vue.prototype.$bus = this
	}
})
```



## 绑定事件

```
//通过on在x身上绑定事件
this.$bus.$on('hello',(data)=>{
	//...
})
```



## 调用事件

```
//在需要触发事件的组件上调用
this.$bus.$emit('hello',data)
```



# 消息订阅



## 安装

> npm i pubsub-js



## 发布消息

```
pubsub.publish('hello',数据)
```



## 订阅消息

```
import pubsub from 'pubsub-js'
	this.pubId = pubsub.subscribe('hello', (msgName, data)=>{
	//函数体写箭头函数或者用this.methods方法，否则this指向pubsub本身
})
```



### 取消订阅

```
pubsub.unsubscribe(this.pubId)
```



# 发送请求



## axios

> 安装 npm i axios

```
import axios from 'axios'
axios.get('').then(
	response => {},
	error => {}
)
```



## resource

> 安装 npm i vue-resource
>
> 不常用

```
import vueResource from 'vue-resource'
//注册插件，之后vue多了个$http属性
Vue.use(vueResource)

//用法跟axios一样
```



# 插槽



## 默认插槽

```
<Student>
	<Hobit>
</Student>
//Hobit组件将作为标签体参数传递给Student组件接收参数

//子组件需要挖一个插槽
//插槽标签<slot>中间是默认值</slot>
```



## 具名插槽

> 多标签插槽

```html
//父组件
<Student>
	//写法1
	<div slot='ho1'></div>
	<div slot='ho2'></div>
	//写法2
	<template v-slot:ho3></template>
</Student>

//子组件
<div>
	<slot name='ho1'></slot>
	<slot name='ho2'></slot>
	<slot name='ho3'></slot>
</div>
```



## 作用域插槽

```
//父组件
<Student>
	<template scope="datax">//scope的值作为接收数据的变量，支持解构赋值
		<ul>
			<li v-for"(d,index) in datax" :key="index">{{d}}</li>
		</ul>
	</template>
</Student>

//子组件定义数据，但不使用数据，而是传给插槽的使用者父组件
<div>
	<slot :datax='datax'></slot>
</div>
exprot default {
	data(){
		return {
			datax:[]
		}
	}
}
```



# Vuex



## 安装

```
npm i vuex
```



## 创建Store

```
/*创建一个store文件*/

import Vue from 'vue'
Vue.use(Vuex)

import Vuex from 'vuex'
const actions = {}
const mutations = {}
const state = {}
const getters = {}
export default new Vuex.Store({
	actions,
	state,
	mutations,
	getters
})
```



## 引入

```
import store from './store'
new Vue({
	store //Vm和vc会带有$store属性
})
```



## dispath更新数据

> dispath与mapActions都是调用action对象的方法
>
> 中间没有逻辑可以忽略dispath，直接commit



### dispath：调用一个action

```
//调用action对象，在对象内进行判断逻辑
.dispath('action_name',value) 
```



### mapActions：映射一组dispath

```
//映射方法mapActions
methods:{
	...mapActions({
		methods_name:'action_name',
		methods_name2:'action_name2',
	}),
	//简写
	...mapActions(['action_name','action_name2']),
}
//通过mapActions生成的映射函数，需要用methods_name('value参数')，而不是用methods_name调用。
```



## commit更新数据

> commit和mapMutations都是更新数据对象Mutations的方法



### commit：调用一个Mutations

```
//更新数据，aciton对象要大写
.commit('ACTION_NAME',value) 
```



### mapMutations：映射一组commit

```
methods:{
    ...mapMutations({
    	//这种方式调用commit会将参数传递给value，而methods默认参数是event，
    	//需要在调用的时候指定value才能避免参数传错。
        methods_name:'ACTION_NAME',
        methods_name2:'ACTION_NAME2'
    })
    //简写
    ...mapMutations([
    	'ACTION_NAME','ACTION_NAME2'
    ])
}

//通过mapMutations生成的映射函数，需要用methods_name('value参数')，而不是用methods_name调用。
//例如
<button @click="methods_name(n)">点击</button>
```



## 操作数据的方法



### state

```
//存储数据，同data属性
const state = {
	sum:0
}
```



### action

```
const action = {
	jia(context, value){ //context是上下文对象，其中包含了用于更新数据的commit的API
		//这里放业务逻辑，通常做一些异步任务，异步请求
		context.commit('JIA',value)
	}
}
```



### mutations

```
const mutations = {
	JIA(state, value){ //state跟data是一个样
		//根据value计算出新的state，state类似于data，作用于数据的使用者
		state.sum += value
	}
}
```





### getters

```
const getters = {
	bigSum(state){
		return state.sum*10
	}
}
```







## 读取数据



### 直接读取

```
//模板中使用
{{$store.state.sum}}
{{$store.getters.bigSum}}
```



### mapState映射状态

```
import {mapState} from 'vuex'
export default {
	computed(){
		//mapState返回一个封装各类state属性和方法的对象，通过...可以展开合并到computed
		...mapState({
			he:'sum',//key写绑定给什么属性，val写数据来自$store.state的哪个属性
		})
		//简写
		...mapState(['sum','......'])
	}
}
```





### mapGetters映射加工状态

```
import {mapGetters} from 'vuex'
export default {
	computed(){
		...mapGetters({
			he:'sum',
		})
		//简写
		...mapGetters(['sum','......'])
	}
}
```



## 模块化



### 配置

```
const countOptions = {
	namespace:true
	state:{},
    getters:{},
    action:{},
    mutations:{},
}
//...各种vue的options
export default new Vuex.Store({
	modules:{
		countAbout:countOptions
	}
})

//读取和操作vuex数据时，通过属性名，也就是coutOptions.data去操作
```



### 读取

```
//直接读取state
this.$store.state.countAbout.data
//直接读取getters
this.$store.getters['countAbout/data']

//读取和操作vuex数据时，通过属性名，countAbout.data去操作
...mapState(['countAbout','...其他数据模块']) //coutOptions.data调用数据

//通过命名空间调用数据
//这种方法namespace为true
...mapState('countAbout',['data','data2','data3']) //data调用数据
...mapState('countAbout',{data_name:data,data2_name:data2}) 
```



### action更新



#### 映射更新数据

> 方法跟commit的命名空间映射方法一样，具体看



#### 单独更新数据

```
this.$store.dispath('countAbout/data',data)
```



### commit更新



#### 映射更新数据

```
...mapMutations(['countAbout','...其他数据模块']) 


...mapMutations('countAbout',['data','data2','data3']) 
...mapMutations('countAbout',{data_name:data,data2_name:data2})
```



#### 单独更新数据

```
this.$store.commit('countAbout/data',data)
//模块化vuex，需要使用命名空间方法，在数据名前加命名空间，然后用/分割
```



# 路由



## 安装

> npm i vue-router



## 配置

```
//创建文件router/index.js
import VueRouter from ‘vue-router’
export default new VueRouter({
	routes:[
	{
		path:'/about',
		component:About //组件
	},
		path:'/about',
		component:About //组件
		children:[ //嵌套路由
			{
				path:'news',
				component:News
			}
		]
	},
	]
})

//引入路由器
import router from '.router'
import VueRouter from 'vue-router'
Vue.use(VueRouter)
export default new Vue({
	router:router
})
```



## 链接

```
<router-link to="/about" active-class='class_name'></router-link>
```



## 视图

```
<router-view></router-view>
```



## 命名

```
export default new VueRouter({
	routes:[
	{
		name:'about',//命名
		path:'/about',
		component:About
	},
	{
		name:'qarams',//给路由声明qarams参数
		path:'/qarams/:value', //value将接收qarams参数
		component:qarams
	},
		path:'/about',
		component:About 
		children:[
			{
				path:'news',
				component:News,
				props:true//为真则将，params将以props的形式传参
			}
		]
	},
	]
})

//使用命名路由
<router-link :to="{
	name:'name'
}">查看</router-link>
```



## query传参



```
//接收数据：
$route.query.key


//传递数据：
//to的常量字符串写法
<router-link to="/?key=value">查看</router-link>

//to的变量字符串写法
<router-link :to="`/?key=${value}`">查看</router-link>

//to的对象写法
<router-link :to="{
	path:'/',
	query:{
		key:value
	}
}">查看</router-link>
```



## params传参

```
//接收数据：
$route.params.value

//路由声明接收：
path:'/qarams/:value' //value将接收qarams参数

//传递数据：
<router-link to="/value/">查看</router-link>
//对象传参
<router-link :to="{
	name:'params', //params传参不允许使用path，必须使用name匹配路由
	params:{
		value:'abc'
	}
}">查看</router-link>
```



## prop传参

```
//布尔值写法：
//路由传递的所有params参数都会通过props床给组件
props:true

//对象写法：
//对象里的key和val会以props的形式传给组件
props:{a:1,b:'hello'}

//函数写法：
//props($route){
	return {id:$route.query.id}
}

//在组件中声明接收
props:['id']
```



## 编程式路由导航



### replace

```
//基本作用
//替换掉路由中的历史记录
<router-link replace to='/abc'></router-link>

//触发replace
this.$router.replace({
	name:'name',//配置路由器动作，相当于点击了下链接
	query:{
		id:'id'
	}
})
```



### push

```
//触发push
this.$router.push({
	name:'name',//配置路由器动作，相当于点击了下链接
	query:{
		id:'id'
	}
})
```



### 前进后退

```
//后退
this.$router.back()

//前进
this.$router.forward()

//前进后退多步
this.$router.go(3)前进3步，负数为后退
```



## 缓存路由

```
<keep-alive>//包裹住路由的组件
	<router-view></router-view>//这个区域的路由导航不会销毁组件，而是进行缓存
</keep-alive>

//筛选缓存组件
<keep-alive include='News'>
	<router-view></router-view>//这个区域的路由导航不会销毁组件，而是进行缓存
</keep-alive>

//筛选缓存多个组件
<keep-alive :include='['News1','News2']'>
	<router-view></router-view>//这个区域的路由导航不会销毁组件，而是进行缓存
</keep-alive>
```



## 路由生命周期

```
//激活路由时执行
activated(){

}

//失活路由时执行
deactivated(){

}
```



## 路由守卫：权限校验



### 全局前置守卫

> 初始化和切换前调用

```
const router = new VueRouter({
	{
		name:'home',
		path:'/home',
		meta:{
			needSuper:true
		}
	}
})

//全局前置路由守卫
router.beforeEach((to, from, next)=>{
	//判断路由
	if(to.meta.needSuper){
        //去localStorage查权限
        if(localStorage.getItem('is_super') === 1){
        	next()//放行
        }else{
        	alert('权限不足')
        }
	}else{
		next()//放行
	}
})
```



### 全局后置守卫

> 初始化和切换后调用

```
const router = new VueRouter({
	{
		name:'home',
		path:'/home',
		meta:{
			needSuper:true
		}
	}
})

//全局后置路由守卫
router.afterEach((to, from)=>{
	//处理一些切换路由后的事情
})
```



### 独享路由守卫

```
const router = new VueRouter({
	{
		name:'home',
		path:'/home',
		beforeEnter:(to, from, next)=>{
			if(localStorage.getItem('is_super') === 1){
                next()//放行
            }else{
                alert('权限不足')
            }
		}
	}
})
```



### 组件内路由守卫

```
export default {
	name:'components',
	//通过路由规则，进入组件时
	beforeRouteEnter(to,from, next){
		//判断进入组件的权限判断
	},
	//通过路由规则，离开组件时
	beforeRouteLeave(to,from, next){
		//判断离开组件的权限判断
	}
}
```



## 路由模式



### history

> 

```
const router = new VueRouter({
	mode:'history', //默认为hash
})
```

#### 解决history后端404问题

> 安装npm i connect-history-api-fallback

```
//修改express
//先use再配置静态资源
app.use(history())
app.use(express.static(__dirname+'/static'))
```





### hash

```
const router = new VueRouter({
	mode:'hash', //默认为hash
})
```



# UI组件库

> 移动端：Vant、Cube UI、mint UI
>
> PC端：Element UI、IView UI
>
> 安装npm i element-ui



## 全部引入

```
import ElementUI from 'element-ui'
import 'element-ui/lib/theme-chalk/index.css'
Vue.use(ElementUI)
```



## 按需引入

> 安装包npm install babel-plugin-component -D
>
> -D为开发依赖

```
//修改babel.config.js
module.exports = {
	presets:[
		...,
		['@babel/preset-env',{"modules":false}],
	],
	plugins:[
		"component",
		{
			"libraryName":'element-ui',
			'styleLibraryName':theme-chalk
		}
	]
}

//修改main.js
//注册组件就行了，不用再引入样式了
import {Button, Row} from 'element-ui'
Vue.component(Button.name,Button)
```



# Vite



> npm init vite-app projectName
>
> 进入文件夹
>
> cd ..
>
> 安装
>
> npm i
>
> 启动
>
> npm dev



# Vue3



## 引入vue

```
import {createApp} from 'vue'
createApp(App).mount(#app)
```



## setup

```js
//App.vue

export default {
	name:'App',
	setup(){
		//数据
		let name = '张三'
        
        //方法
        function sayHello(){
            alert(`我是${name}`)
        }
        
        //返回一个对象
        return {
            name,
            sayHello
        }
        
        //返回一个函数
        //需要引入h，import {h} from 'vue'
        return()=> h('h1','abc')
	}
}
```



## setup参数

```js
//App.vue

export default {
	name:'App',
    props:['p1']
	emits:['hello'] //声明接收自定义事件
	setup(props, context){ //context对象包含emits自定义事件
		context.attrs
		context.slots
		context.emit
        return {}
	}
}
```



## 计算属性

```js
import {computed} from 'vue'
export default {
	setup(){
		let person = reactive({
			firstName:'a',
			lastName:'b'
		})
		//简写，无法修改
		person.fullName = compute(()=>{
			return person.firstName + '-' + person.lastName
		})
        //完整写法
		person.fullName = compute(()=>{
            get(){
				return person.firstName + '-' + person.lastName
            },
            set(value){
                ...//更新逻辑
            }
		})
	}
}
```



## 监视属性

```js
import {ref,watch} from 'vue'
export default {
	setup(){
		let sum = ref(0)
		let abc = ref('a')
		//监视一个数据
		watch(sum, (newValue, OldValue)=>{
		}, {immediate:true,deep:true})
        //监视多个
		watch([sum, abc], (newValue, OldValue)=>{
		})
		//如果监视器监视的是reactive定义的数据，将无法得到oldValue
	}
}
```



## watchEffect监视

```
import {watchEffect} from 'vue'
watchEffect(()=>{
	const x1 = sum.value //监视sum.value
})
```



## ref：处理响应式基本数据、对象、数组

```
//App.vue
import {ref} import 'vue'

export default {
	name:'App',
	setup(){
		//数据
		let name = ref('张三')
		let job = ref({
			type:'前端',
			salary:'30k'
		})
        
        //方法
        function sayHello(){
        	name.value = '李四'
        	job.value.type = '后端'
            alert(`我是${name}`)
        }
        
        //返回一个对象
        return {
            name,
            sayHello
        }
	}
}
```



## reactive：处理响应式数据对象、数组

```
//App.vue
import {ref,reactive} import 'vue'

export default {
	name:'App',
	setup(){
		//数据
		let name = ref('张三')
		let job = reactive({
			type:'前端',
			salary:'30k'
		})
        
        //方法
        function sayHello(){
        	name.value = '李四'
        	job.type = '后端'
            alert(`我是${name}`)
        }
        
        //返回一个对象
        return {
            name,
            sayHello
        }
	}
}
```



# 扩展



## 特殊生命周期钩子：下一轮执行$nextTick

```
this.$nextTick(function(){
	//再下一次更新dom后再执行
	//类似于定时器任务做的延迟任务
})
```



## 动画效果



```
@keyframes test{
	from {
		transform:translateX(-100%);
	}
	to {
		transform:translateX(0px);
	}
}

.v-enter-active{
	animation:test 1s;
}
.v-leave-active{
	animation:test 1s reverse;/*reverse是取反*/
}

//实现动画
//通过动态修改div类名切换，实现动画效果
//也可以通过vue的transition标签实现
<transition name='name' :appear='true'>//appear为加载时触发动画，name为css类名v的前缀
	<div v-show='isShow'>hi</div>
</transition>
//isShow数据改变时，触发动画
```



## 过度效果

```
.v-enter-active, .v-leave-active{
	transition:0.5s linear;/*linear是否匀速*/
}

.v-enter, .v-leave-to{//进入的起点 和离开的重点
	transform:translateX(-100%)
}
.v-enter-to, .v-leave{//进入的终点 和离开的起点
	transform:translateX(0)
}

//实现动画
//通过动态修改div类名切换，实现动画效果
//也可以通过vue的transition标签实现
<transition name='name' :appear='true'>//appear为加载时触发动画，name为css类名v的前缀
	<div v-show='isShow'>hi</div>
</transition>
//isShow数据改变时，触发动画
```



## 多元素过度

> transition改为transition-group，并且加key值



## 三方动画

> animate.css
>
> 安装npm i animate.css
>
> import 'animate.css'
>
> 用法看官网



# Express



## 安装

> npm i express



## server

```
//创建server.js

const express = require('express')

const app =express()
//指定静态资源
app.use(express.static(__dirname+'/static'))
//配置路由
app.use('person',(req,res)=>{
	res.send({name:'tom'})
})
app.listen(5005,(err)=>{
	if(!err) console.log('开启')
})
```



# 开发者工具

> Vue.js devtools bets
>
> Vue.js devtools



# Vscode插件

> vue 3 snippets 代码片段 作者：hollowtree

 

# JS语法



## 数组过滤

```js
persons.filter((p)=>{
	return p.name.indexOf(val) !== -1
    //p.name.indexOf(val)
    //判断p中是否包含val ，返回-1为不包含，返回其他则为匹配值的索引
})
```



## 数组排序

```js
arr.sort((a,b)=>{
	return a-b //升序
	return b-a //降序
})
```



## 随机数

> uuid
>
> npm i nanoid

```
import {nanoid} from ‘namoid’
```

