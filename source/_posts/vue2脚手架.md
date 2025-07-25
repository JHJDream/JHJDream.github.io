---
title: Vue2比较
date: 2023-09-06
---

# 1. Vue脚手架

## 脚手架文件结构

	├── node_modules 
	├── public
	│   ├── favicon.ico: 页签图标
	│   └── index.html: 主页面
	├── src
	│   ├── assets: 存放静态资源
	│   │   └── logo.png
	│   │── component: 存放组件
	│   │   └── HelloWorld.vue
	│   │── App.vue: 汇总所有组件
	│   │── main.js: 入口文件
	├── .gitignore: git版本管制忽略的配置
	├── babel.config.js: babel的配置文件
	├── package.json: 应用包配置文件 
	├── README.md: 应用描述文件
	├── package-lock.json：包版本控制文件

## 关于不同版本的Vue

1. vue.js与vue.runtime.xxx.js的区别：
    1. vue.js是完整版的Vue，包含：核心功能 + 模板解析器。
    2. vue.runtime.xxx.js是运行版的Vue，只包含：核心功能；没有模板解析器。
2. 因为vue.runtime.xxx.js没有模板解析器，所以不能使用template这个配置项，需要使用render函数接收到的createElement函数去指定具体内容。

## vue.config.js配置文件

1. 使用vue inspect > output.js可以查看到Vue脚手架的默认配置。
2. 使用vue.config.js可以对脚手架进行个性化定制，详情见：https://cli.vuejs.org/zh

## ref属性

1. 被用来给元素或子组件注册引用信息（id的替代者）
2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）
3. `this.$refs`是一个对象，即每个ref的集合
4. 使用方式：
    1. 打标识：```<h1 ref="xxx">.....</h1>``` 或 ```<School ref="xxx"></School>```
    2. 获取：```this.$refs.xxx``` 

## props配置项

1. 功能：让组件接收外部传过来的数据

2. 传递数据：```<Demo name="xxx"/>```

3. 接收数据：

    1. 第一种方式（只接收）：```props:['name'] ```

    2. 第二种方式（限制类型）：```props:{name:String}```

    3. 第三种方式（限制类型、限制必要性、指定默认值）：

        ```js
        props:{
        	name:{
        	type:String, //类型
        	required:true, //必要性
        	default:'七七' //默认值
        	}
        }
        ```

    > 备注：props是只读的，Vue底层会监测你对props的修改，如果进行了修改，就会发出警告，若业务需求确实需要修改，那么请复制props的内容到data中一份，然后去修改data中的数据。

## mixin(混入)

1. 功能：可以把多个组件共用的配置提取成一个混入对象

2. 使用方式：

    第一步定义混合：（新建一个和main.js同级的mixin.js文件）

    ```js
    export const xxx = {
        data(){....},
        methods:{....}
        ....
    }
    ```

    第二步使用混入：

    ​	全局混入：```Vue.mixin(xxx)```（写在main.js里）
    ​	局部混入：```mixins:[xxx]	```（写在组件里）
    
3. 一般在原组件和xxx中共有的属性会优先选择原组件的属性值

    如果还写了mounted挂载，则不是择其一，而是都采用，但xxx中的mounted会先执行

    执行次数：如果是全局混入，则是1+n次（1个vm+n个vc，它们都要挂载）；局部混入就看有多少个vc引入了这个混入

## 插件

1. 功能：用于增强Vue

2. 本质：包含install方法的一个对象，install的第一个参数是Vue，第二个以后的参数是使用者传递的数据。

3. 定义插件：（一般新建一个和main同级的plugins.js文件，在里面配置）

    ```js
    export default {
        对象.install = function (Vue, options) {
            // 1. 添加全局过滤器
            Vue.filter(....)
    
            // 2. 添加全局指令
            Vue.directive(....)
    
            // 3. 配置全局混入(合)
            Vue.mixin(....)
    
            // 4. 添加实例方法
            Vue.prototype.$myMethod = function () {...}
            Vue.prototype.$myProperty = xxxx
        }
    }
    ```

4. 使用插件：```Vue.use(plugins, options)``` （写在main.js里）

## scoped样式

1. 作用：让样式在局部生效，防止冲突。
2. 写法：```<style scoped>``` （App.vue中一般不写scoped）

## 总结TodoList案例

1. 组件化编码流程：

    ​	(1).拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。

    ​	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

    ​			1).一个组件在用：放在组件自身即可。

    ​			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

    ​	(3).实现交互：从绑定事件开始。

2. props适用于：

    ​	(1).父组件 ==> 子组件 通信

    ​	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！

4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。

## webStorage

1. 存储内容大小一般支持5MB左右（不同浏览器可能还不一样）

2. 浏览器端通过 `Window.sessionStorage` 和 `Window.localStorage` 属性来实现本地存储机制。

3. 相关API：

    1. ```xxxxxStorage.setItem('key', 'value');```
        					该方法接受一个键和值作为参数，会把键值对添加到存储中，如果键名存在，则更新其对应的值。

    2. ```xxxxxStorage.getItem('person');```

        ​		该方法接受一个键名作为参数，返回键名对应的值。

    3. ```xxxxxStorage.removeItem('key');```

        ​		该方法接受一个键名作为参数，并把该键名从存储中删除。

    4. ``` xxxxxStorage.clear()```

        ​		该方法会清空存储中的所有数据。

4. 备注：

    1. SessionStorage存储的内容会随着浏览器窗口关闭而消失。
    
    2. LocalStorage存储的内容，需要手动清除才会消失。
    
    3. ```xxxxxStorage.getItem(xxx)```如果xxx对应的value获取不到，那么getItem的返回值是null。
    
       `JSON.parse(localStorage.getItem('todos')) || []` 一般这样写避免报错
    
    4. ```JSON.parse(null)```的结果依然是null。

## 组件的自定义事件

1. 一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>

2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。

3. 绑定自定义事件：

    1. 第一种方式，在父组件中：```<Demo @atguigu="test"/>```  或 ```<Demo v-on:atguigu="test"/>```

    2. 第二种方式，在父组件中：（更灵活，比如可以添加绑定事件的条件→定时器延时等）

        ```js
        <Demo ref="demo"/>
        ......
        mounted(){
           this.$refs.xxx.$on('atguigu',this.test)
            // this.$refs.xxx.$once('atguigu',this.test) //绑定自定义事件（一次性）
        }
        ```

    3. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。

4. 触发自定义事件：```this.$emit('atguigu',数据)``` （在子组件中）

5. 解绑自定义事件```this.$off('atguigu') ``` （在子组件中）

    ```js
    this.$off('atguigu') //解绑一个自定义事件
    this.$off(['atguigu','demo']) //解绑多个自定义事件
    this.$off() //解绑所有的自定义事件
    ```

6. 组件上也可以绑定原生DOM事件，需要使用```native```修饰符，否则会当成自定义事件

7. 注意：通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！

8. 回调得留在父组件中

## 全局事件总线（GlobalEventBus）

- 一个重要的内置关系：`VueComponent.prototype.__proto__ === Vue.prototype` 所有vm和vc都能看到Vue.prototype

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>

2. 安装全局事件总线：（在main.js中安装，'在哪引入的Vue你心里还没点abcd数吗？'）

   ```js
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo) // 或者直接在这里写箭头函数
      }
      ```

   2. 提供数据：（触发事件）

      ```js
      this.$bus.$emit('xxxx',数据)
      ```

4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。

5. 之前自定义事件中没有解绑，是因为事件是绑定给组件，组件不用了，事件自然也就不在了；

   但是全局时间总线中，事件是绑定给$bus的，组件不用了，但事件还在，所以需要解绑

6. 组件间通信：

   - 父组件 → 子组件：props
   - 子组件 → 父组件：props 或 自定义事件
   - 祖孙、兄弟组件之间：全局事件总线（消息订阅与发布用得不多，因为与全局事件总线差不多，但用了插件）

## 消息订阅与发布（pubsub）

1.   一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：```npm i pubsub-js```

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(_, data){......} // 因为会收到消息名，所以用_占位，如果写msgName的话，不用不好，是暗的
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据（发布消息）：```pubsub.publish('xxx',数据)```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>
## nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。

```js
this.$nextTick(function() {
	this.$refs.inputTitle.focus()
})
```



## Vue封装的过渡与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

2. 图示：![Vue封装的过渡与动画](.\images\Vue封装的过渡与动画.png)

3. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

      ```css
      /** 用动画 **/
      .hello-enter-active{ // 因为配置了name属性，所以v改为name的属性值hello
      	animation: atguigu 0.5s linear;
      }
      .hello-leave-active{
      	animation: atguigu 0.5s linear reverse;
      }
      @keyframes atguigu {
      	from{
      		transform: translateX(-100%);
      	}
      	to{
      		transform: translateX(0px);
      	}
      }
      /** 或者用过渡transition **/
      /* 进入的起点、离开的终点 */
      .hello-enter,.hello-leave-to{
      	transform: translateX(-100%);
      }
      /* 进入和离开的过程，写在这里就不用破坏h1本来的样式，当然直接写在h1的样式里也行 */
      .hello-enter-active,.hello-leave-active{ 
      	transition: 0.5s linear;
      }
      /* 进入的终点、离开的起点 */
      .hello-enter-to,.hello-leave{
      	transform: translateX(0);
      }
      ```
   
   2. 使用```<transition>```包裹要过度的元素，并配置name属性：
   
      ```vue
      <transition name="hello" appear>
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```
   
   3. 备注：
   
      - apper属性可以控制一上来就启用动画 `:appear:"true"` 可以简写为 `appear` 就表示添加这个属性且值为true
   
      - 若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。
   
      ```html
      <transition-group name="hello" appear>
      	<h1 v-show="!isShow" key="1">你好啊！</h1>
      	<h1 v-show="isShow" key="2">尚硅谷！</h1>
      </transition-group>
      ```
   
   4. 使用第三方库：
   
      npm中有很多插件，关于动画推荐`animate.css`，直接在npm中搜就行，然后点击HomePage跳转到官网，查看其具体使用方法
   
      - 安装：`npm install animate.css`
      - 引入：`import 'animate.css'`
      - 使用：`<h1 class="animate__animated animate__bounce">An animated element</h1>`
   
      其官网顶部右边有个导航栏，点击即可在左边查看对应的动画，点击复制类名，如下所示粘贴到`xxx-class=""`的引号里使用即可
   
      ```html
      <transition-group 
      	appear
      	name="animate__animated animate__bounce" 
      	enter-active-class="animate__swing"
      	leave-active-class="animate__backOutUp"
      >
      	<h1 v-show="!isShow" key="1">你好啊！</h1>
      	<h1 v-show="isShow" key="2">尚硅谷！</h1>
      </transition-group>
      ```

# 2. Vue中的ajax

## vue脚手架配置代理

### 方法一

​	在vue.config.js中添加如下配置：

```js
devServer:{
  proxy:"http://localhost:5000"
}
```

​	在.vue文件的methods中：

```js
getStudents(){
	axios.get('http://localhost:8080/students').then( // 向端口号8080请求数据students
		response => {
			console.log('请求成功了',response.data)
		},
		error => {
			console.log('请求失败了',error.message)
		}
	)
},
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源，也就是public文件夹里面的资源）

### 方法二

​	编写vue.config.js配置具体代理规则：

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'（请求前缀）开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        // ws: true, //用于支持websocket
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true，即返回一个假的localhost:5000
*/
```

```js
axios.get('http://localhost:8080/atguigu/students').then()
```

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理，走代理时加前缀 (紧跟在端口号后面)，不走则不加。
2. 缺点：配置略微繁琐，请求资源时必须加前缀。

## 插槽

1. 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 <strong style="color:red">父组件 ===> 子组件</strong> 。

2. 分类：默认插槽、具名插槽、作用域插槽

3. 理解：父组件中把子组件写成双标签形式，在里面写上内容，在子组件定义插槽后就会将该内容插入到子组件的指定位置，至于样式，写在父组件或子组件里都可

   - 写在父组件中：解析后的结构带着样式插入插槽
   - 写在子组件中：解析后只把结构插入插槽，样式在子组件中控制

4. 使用方式：

   1. 默认插槽：

      ```vue
      父组件中：
              <Category> <!-- category分类的意思 -->
                 <div>html结构1</div>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot>插槽默认内容...</slot>
                  </div>
              </template>
      ```

   2. 具名插槽：

      ```vue
      父组件中：
              <Category>
                  <template slot="center"> <!-- 如果写多个center也不会覆盖，都会被写到插槽里 -->
                    <div>html结构1</div>
                  </template>
      
                  <template v-slot:footer> <!-- v-slot这种写法只能写在template里，是新的api -->
                     <div>html结构2</div>
                  </template>
              </Category>
      子组件中：
              <template>
                  <div>
                     <!-- 定义插槽 -->
                     <slot name="center">插槽默认内容...</slot>
                     <slot name="footer">插槽默认内容...</slot>
                  </div>
              </template>
      ```

   3. 作用域插槽：

      1. 理解：<span style="color:red">数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。</span>（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）把子组件数据给父组件

      2. 具体编码：

         注：scope是旧api，slot-scope是新api，两个一样，用哪个都行；作用域插槽也能起名字
         
         ```vue
         父组件中：
         		<Category>
         			<template scope="scopeData"> <!-- 或写成scope="{games}" -->
         				<!-- 生成的是ul列表 -->
         				<ul>
         					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
         				</ul>
         			</template>
         		</Category>
         
         		<Category>
         			<template slot-scope="scopeData">
         				<!-- 生成的是h4标题 -->
         				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
         			</template>
         		</Category>
         子组件中：
                 <template>
                     <div>
                         <slot :games="games"></slot> <!--可以传多个值，用的时候scopeData.xxx就行-->
                     </div>
                 </template>
         		
                 <script>
                     export default {
                         name:'Category',
                         props:['title'],
                         //数据在子组件自身
                         data() {
                             return {
                                 games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                             }
                         },
                     }
                 </script>
         ```

# 3. Vuex

### 1.概念

​		在Vue中实现`集中式状态（数据）管理`的一个`Vue插件`，对vue应用中`多个组件的共享状态`进行集中式的管理（读/写），也是一种组件间通信的方式，且`适用于任意组件间通信`。

​		因为是插件，所以须先安装 `npm i vuex`

​		Github 地址: `https://github.com/vuejs/vuex`

### 2.何时使用？

		1. 多个组件依赖于同一状态 
		2. 来自不同组件的行为需要变更同一状态

  即多个组件需要`共享数据`时

### 3.搭建vuex环境

1. 创建文件：```src/store/index.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //应用Vuex插件
   Vue.use(Vuex)
   
   //准备actions对象——响应组件中用户的动作
   const actions = {}
   //准备mutations对象——修改state中的数据
   const mutations = {}
   //准备state对象——保存具体的数据
   const state = {}
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions, //键与值重名，触发对象的简写形式
   	mutations,
   	state
   })
   ```

2. 在```main.js```中创建vm时传入```store```配置项

   注意：脚手架解析时会先把所有的import按代码编写顺序全部汇总到最上方，一一引入后再来读取别的语句，而创建store前须先应用Vuex，所以不能把Vue.use(Vuex)写在main.js中，而main.js中也无须引入Vuex
   
   ```js
   ......
   //引入store
   import store from './store' //默认引入里面的index.js文件，如果没有该文件则不能省略文件名，否则会报错
   ......
   
   //创建vm
   new Vue({
   	el:'#app',
   	render: h => h(App),
   	store
   })
   ```

###    4.基本使用

1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

   ```js
   //引入Vue核心库
   import Vue from 'vue'
   //引入Vuex
   import Vuex from 'vuex'
   //引用Vuex
   Vue.use(Vuex)
   
   const actions = {
       //响应组件中加的动作（没有业务逻辑）
   	jia(context,value){ // 第一个参数是上下文，第二个参数是接收到的值
   		// console.log('actions中的jia被调用了',context,value)
   		context.commit('JIA',value)
   	},
       //当sum为奇数时执行加动作（有判断的业务逻辑）
       jiaOdd(context, value) {
           console.log('actions中的jiaOdd被调用了')
           if (context.state.sum % 2) {
               context.commit('JIA', value)
           }
       },
   }
   
   const mutations = {
       //执行加
   	JIA(state,value){ //一般这里的函数名用大写，便于与actions区分，且因为它能直接操作state
   		// console.log('mutations中的JIA被调用了',state,value)
   		state.sum += value
   	}
   }
   
   //初始化数据
   const state = {
      sum:0
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	actions,
   	mutations,
   	state,
   })
   ```

2. 组件中读取vuex中的数据：```$store.state.sum```

3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

   >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```
   
   ```js
   increment(){
   	this.$store.commit('JIA',this.n)
   },
   incrementOdd(){
   	this.$store.dispatch('jiaOdd',this.n)
   }
   ```

### 5.getters的使用

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。（可以不用getters，但逻辑复杂须复用时建议用getters加工）

2. 在```store.js```中追加```getters```配置

   ```js
   ......
   
   const getters = {
   	bigSum(state){
   		return state.sum * 10
   	}
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	......
   	getters
   })
   ```

3. 组件中读取数据：```$store.getters.bigSum```

4. state 与 getters 的关系就像 data 和 computed，getters 和 computed 都是拿原数据进行加工

### 6.四个map方法的使用

- 在组件中引入map方法：

  ```js
  import {mapState,mapGetters,...} from 'vuex'
  ```

- 自己写的计算属性会出现在`computed`里，虽然借助map生成的计算属性也隶属于`computed`，但会出现在开发者工具的`vuex bindings`里

- 注意：map方法里的对象要写成`xxx:'xxx'`的形式，键的引号可省略（当然也可以不省略），但值的引号不能省，否则会去找xxx变量，但它其实是字符串，因此也不能用对象的简写形式

- 数组写法['xxx']的'xxx'表示：将state里读取的属性'xxx'映射为计算属性，且计算属性名也为'xxx'，所以使用时也须写成xxx

1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性（使用时就不用`$store.state.sum`写这么长了）

   ```js
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}), //解构赋值，将这个对象里的三个函数结构出来放到computed里
            
       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

   ```js
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),
   
       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

3. <strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：incrementOdd、incrementWait（对象形式）
       ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   
       //靠mapActions生成：jiaOdd、jiaWait（数组形式）
       ...mapActions(['jiaOdd','jiaWait'])
   }
   ```

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。
>
> ```html
> <button @click="increment(n)">+</button>
> <button @click="decrement(n)">-</button>
> <button @click="incrementOdd(n)">当前求和为奇数再加</button>
> <button @click="incrementWait(n)">等一等再加</button>
> ```

### 7.模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. modules 

   - 包含多个 module
   - 一个 module 是一个 store 的配置对象 
   - 与一个组件（包含有共享数据）对应

3. 修改```store.js```

   ```javascript
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){
          return state.sum * 10
       }
     }
   }
   
   const personAbout = {
     namespaced:true,//开启命名空间
     state:{ ... },
     mutations: { ... },
     actions: { ... }
   }
   
   export default new Vuex.Store({
     modules: {
       countAbout, // 对象的简写形式
       personAbout
     }
   })
   ```

4. 开启命名空间后，组件中读取state数据：

   ```js
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ```

5. 开启命名空间后，组件中读取getters数据：

   ```js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

6. 开启命名空间后，组件中调用dispatch

   ```js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

7. 开启命名空间后，组件中调用commit

   ```js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```

8. 也可以把每个模块写成一个js文件放在store文件夹里

   ```js
   // 在index.js中引入
   import countAbout from './count';
   import personAbout from './person'
   ```

   ```js
   // 在 count.js 和 person.js 中采用默认暴露
   export default {
       namespaced: true,
       state: {},
       actions: {},
       mutations: {},
       getters: {}
   }
   ```

# 4. 路由

1. 理解： 一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. 前端路由：key是路径；value是`组件component`，用于`展示页面内容`。当浏览器的路径改变时, 对应的组件就会显示
3. 后端路由：key是路径；value是`函数function`，用于`处理客户端提交的请求`。服务器接收到一个请求时, 根据请求路径找到匹配的函数 来处理请求, 返回响应数据
4. vue-router 的理解：vue 的一个插件库，专门用来实现 SPA 应用

![路由和路由器](.\images\路由和路由器.png)

![前端路由工作流程](.\images\前端路由工作流程.png)

### 1.基本使用

1. 安装vue-router，命令：```npm i vue-router```

2. 应用插件：```Vue.use(VueRouter)```

3. main.js中：

   ```js
   ...
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入路由器
   import router from './router'
   
   //应用插件
   Vue.use(VueRouter)
   
   //创建vm
   new Vue({
       el: '#app',
       render: h => h(App),
       router
   })
   ```

4. 编写router配置项:

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({ // 或者export default new VueRouter({...})
   	routes:[{
   		path:'/about',
   		component:About
   	},{
   		path:'/home',
   		component:Home
   	}]
   })
   
   //暴露router
   export default router
   ```

5. 实现切换（active-class="xxx"可配置高亮样式，点击后加上样式.xxx）`<router-link>`最终会被转成`<a>`标签

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

6. 指定展示位置

   ```vue
   <router-view></router-view>
   ```

### 2.几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息（每个组件都有`$route`属性，是不一样的）。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到（每个组件都有`$router`属性，不过是同一个）。

### 3.多级路由（嵌套路由）

1. 配置路由规则，使用children配置项：

   ```js
   routes:[ // 一级路由
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```vue
   <router-link to="/home/news">News</router-link>
   ```

### 4.路由的query参数

1. 传递参数(加个'?x=xxx&y=yyy')

   ```vue
   <!-- 跳转并携带query参数，to的字符串写法(上面的只能传固定参数，下面的可以传变量，用模板字符串) 
   	用:绑定后，引号""里面的内容会被解析为js表达式-->
   <router-link to="/home/message/detail?id=666&title=你好">跳转</router-link>
   <router-link :to="`/home/message/detail?id=${m.id}&title=${m.title}`">{{m.title}}</router-link>
   				
   <!-- 跳转并携带query参数，to的对象写法 建议用这种，没这么乱-->
   <router-link 
   	:to="{
   		path:'/home/message/detail', // 写到组件就行
   		query:{ // 参数在这个配置项里写
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```js
   $route.query.id
   $route.query.title
   ```
   
   ```html
   <li>消息编号：{{$route.query.id}}</li>
   <li>消息标题：{{$route.query.title}}</li>
   ```

### 5.命名路由

1. 作用：可以简化路由的跳转（在路径复杂时）。

2. 如何使用 (用name跳转时必须写成对象形式，不能是字符串)

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                            name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```vue
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>
      
      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>
      
      <!--简化写法配合传递参数 -->
      <router-link 
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
                  title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```

### 6.路由的params参数

1. 配置路由，声明接收params参数

   ```js
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```vue
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！

3. 接收参数：

   ```js
   $route.params.id
   $route.params.title
   ```

### 7.路由的props配置

​	作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件，值是死的
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props(route){ // 接收到的参数就是$route
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```

### 8.```<router-link>```的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为```push```和```replace```，```push```是追加历史记录，```replace```是替换当前记录。路由跳转时候默认为```push```
3. 如何开启```replace```模式：```<router-link replace .......>News</router-link>``` (或者 `:replace="true"`，不过没必要)

### 9.编程式路由导航

1. 作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
   //this.$router.push(path): 相当于点击路由链接(可以返回到当前路由界面) 
   this.$router.push({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   //this.$router.replace(path): 用新路由替换当前路由(不可以返回到当前路由界面) 
   this.$router.replace({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   
   this.$router.forward() //前进  请求(返回)上一个记录路由
   this.$router.back() //后退
   this.$router.go() //可前进也可后退 go中要传一个参数，n/-n表示向前/后跳转n个页面
   //this.$router.go(-1): 请求(返回)上一个记录路由
   //this.$router.go(1): 请求下一个记录路由
   ```

### 10.缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```vue
   <!-- 缓存一个路由组件 -->
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   
   <!-- 缓存多个路由组件 -->
   <!-- <keep-alive :include="['News','Message']"> -->
   ```
   
3. 用`<keep-alive>`包裹`要保持挂载的路由组件的`展示区`<router-view>`，include里写的是组件名，表示要让哪个组件保持挂载，不写include就表示该展示区的所有路由组件都保持挂载，在切换路由组件时不被销毁

### 11.两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. ```activated```路由组件被激活时触发。(比如从别的路由组件切换到当前路由组件)
   2. ```deactivated```路由组件失活时触发。(比如从当前路由组件切走)

### 12.路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫: 配置在路由器中

   ```js
   const router =  new VueRouter({ //创建一个路由器，不直接就暴露，先用router接收
       routes: [
           ...
           {
               name: 'xinwen',
               path: 'news',
               component: News,
               meta: { isAuth: true, title: '新闻' } //meta是路由元信息，由程序员自己配置的信息
           }, //若无须权限控制，则isAuth值为false，也可以直接不写isAuth，取不到isAuth的值自然就返回false
           ...
       ]
   })
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{ //to目标路径, from来源路径
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制(鉴权)
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{ //后置路由守卫没有next
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{ // 一上来什么都没点的 什么路由组件都不展示的时候
   		document.title = 'vue_test'
   	}
   })
   //暴露路由器
   export default router
   ```

4. 独享守卫:（没有后置路由守卫，所以就叫独享守卫没有前置后置之分）配置在路由中（与name、... 、meta同级）

   ```js
   beforeEnter(to,from,next){
   	console.log('beforeEnter',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){
   			next()
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next()
   	}
   }
   ```

5. 组件内守卫：（没有前置后置的说法，只有进入和离开）（官方说beforeRouteEnter是activated的替代）

   ```js
   //进入守卫：通过路由规则，进入该组件时被调用，也就是to与该组件相关时
   beforeRouteEnter (to, from, next) {
   },
   //离开守卫：通过路由规则，离开该组件时被调用，也就是from与该组件相关时
   beforeRouteLeave (to, from, next) {
   }
   ```
   
6. 生命周期执行顺序beforeEach→beforeEnter→beforeRouterEnter

### 13.路由器的两种工作模式

1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。
2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。
3. hash模式：
   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。
4. history模式：
   1. 地址干净，美观 。
   2. 兼容性和hash模式相比略差。
   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。npm网站中的插件connect-history-api-fallback可以解决这个问题
	
	 

