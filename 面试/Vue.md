### Vue复习中...



#### MVVM

Model、View、ViewModel

ViewModel层数据的双向绑定，①模型(model) 转化为视图(view)，后端传递的数据渲染至页面，实现方式为数据绑定；②数据绑定视图转化为模型，页面传递数据给后端，实现方式DOM事件监听。

MVVM使得view model自动同步，当model改变时，不需要手动操作dom元素，view展示改变属性后的视图层，也就是数据驱动视图的思想。



#### 为什么 data 是一个函数

防止数据污染组件的数据空间，data设计成一个函数返回值形式，每次复用组件，就会形成一个新的私有数据空间，每个组件就能维护各自的数据，从而防止共用同一份数据，造成一个变量改变，所有的都改变。



#### Vue 组件通讯有哪几种方式

1. props和$emit 父组件向子组件传递数据，子组件使用props接收；子组件传递数据给父组件，使用$emit触发通知父组件来实现。
2. 父组件通过provide向子组件注入数据，所有的子组件都能使用inject来接受父组件传递的数据。
3. $attrs和$listeners A => B => C，子组件能接受父组件传下来的props值，不必从B组件中转，$listeners能监听父组件v-on绑定的事件，不包含.natvie
4. $refs获取组件实例
5. vuex状态管理
6. eventBus事件总线



#### Vue 的生命周期方法有哪些 一般在哪一步发请求

1. beforeCreate 实例初始化后，数据观测之前，此时data、methods、computed、watch不能被访问到
2. Created 实例已经创建完成后被调用，这一步中，数据观测(data observer)，属性和方法运算，watch/event回调，无法和DOM进行交互，可以通过vm.$nextTick访问DOM
3. beforeMount 实例挂载之前调用，相关的render函数首次调用
4. Mounted 实例挂载完成调用，当前阶段，DOM挂载完毕，数据双向绑定，可以访问DOM节点
5. beforeUpdate 数据更新时调用，在虚拟DOM渲染之前调用，此时还可以更改状态
6. Updated 数据更新结束后调用，此时DOM渲染完成，需要避免在这个阶段更改数据，可能会导致无限循环更新
7. beforeDestory 实例销毁之前调用，此时实例还可以调用，这个时候可以进行清除定时器
8. destoryed 实例销毁后调用，实例的所有指令被解绑，事件监听被移除，子实例也会销毁
9. activated keep-alive 专属， 组件被激活时调用
10. deactivated keep-alive专属，组件被销毁时调用



异步请求在哪一个钩子中执行？

可以在created、beforeMount、mounted中进行异步请求，因为3给钩子的实例已经创建，可以访问data中的属性，可以将服务端返回的数据进行赋值操作

异步请求不需要与DOM绑定，可以在created中进行请求，减少loading时间



#### v-if 和 v-show 的区别

v-if编译过程中会被转化成三元表达式，不满足条件的节点不会被渲染

v-show会被编译成指令，条件不满足时，将进行节点隐藏，display：none

使用场景：

v-if适用于很少改变的情况，不需要频繁更新的情况

v-show适用于频繁更新的情况



#### Vue内置指令

- v-once：定义的元素或组件只渲染一次，不再随数据变化而变化，视为静态内容
- v-bind：绑定属性，动态更新HTML元素上的属性 例如：v-bind: class
- v-on：用于监听DOM时间，例如 click、keyup
- v-html：赋值变量就是innerHTML，需要防止xss攻击
- v-text：更新元素的内容
- v-model：语法糖，变成value与input的语法糖
- v-if、v-else-if、v-else：配合template使用，使用三元表达式
- v-show：显示隐藏元素
- v-for：循环列表，优先级比v-if高，需要绑定key值



#### 理解Vue单向数据流

数据总要从父组件传递给子组件，而子组件没有权限更改父组件传递来的数据，只能请求父组件进行数据更新，再传递回来，可以防止子组件由于不当操作更改父组件的状态，从而导致无法理解数据流。



#### computed与watch使用场景

computed 计算属性，当以来的数据计算值发生改变，则更新属性，且会有缓存值，只有依赖的计算值发生变化才会返回，可以设置getter和setter



watch 监听值的变化，来更新属性，在回调函数中可以进行操作

computed是用来监听其他响应式对象计算值的变化，来对需要返回的属性进行更新；监听适用于观测某个值发生变化来更新，来完成某种复杂的业务。



------



#### Vue2.0 响应式数据的原理

数据劫持 与 观察值模式

主要使用了Object.defineProperty方法进行属性劫持，数组会通过重写数组方法来实现。



#### vue3.0 用过吗 了解多少

- 响应式原理更新，Vue3.0使用Proxy 取代 Vue2.x 版本的 Object.defineProperty
- 组件选项声明方式 Vue3使用了 CompositionAPI 和 setup函数，让代码模块更聚合
- 模板语法变化 slot具名插槽，自定义指令v-model升级
- Vue3支持多个根节点



#### Vue3.0 和 2.0 的响应式原理区别

Vue3.x 使用 Proxy 代替了 Object.defineProperty，使得Vue可以监听数组和对象的变化，且有更多的拦截方法



#### Vue 的父子组件生命周期钩子函数执行顺序

加载渲染过程

父组件 beforeCreate --> 父组件 created --> 父组件 beforeMount --> 子组件 beforeCreate -->子组件created -->子组件 beforeMount -->子组件 mounted --> 父组件mounted

加载、更新、销毁，都是以父组件结束



#### 虚拟 DOM 是什么 有什么优缺点

由于浏览器中操作DOM的成本很昂贵，会进行重绘重排，浪费性能，虚拟DOM就是为了减少性能开支而产生的。

优点：

- 保证性能下限：框架的虚拟DOM需要适配任何上层API可能产生的操作，它的一些DOM操作是普适的，所以它的性能不是最优的，但比起粗暴的操作DOM来说，能保证你在不进行任何优化下，保持一定的性能优化，确定了下限
- 无需操作DOM：无需手动操作DOM，只需要在ViewModel处理好数据后，框架会根据虚拟DOM来进行双向数据绑定，更新视图，提高开发效率



缺点：

- 首次渲染大量DOM时，多了一层虚拟DOM的计算，会比innerHTML插入慢



#### v-model 原理

v-model是语法糖



#### v-for 为什么要加 key

通过给vnode绑定key值，进行唯一标记，进行diff算法时，操作可以更快，给需要变化的vnode进行更新，其他vnode进行复用



#### Vue 事件绑定原理

原生事件是通过addEventListener绑定给真实元素，Vue组件通过自定义的$on事件进行绑定。如果组件需要绑定原生事件，需要加.native修饰符，将组件当成一个普通的HTML标签，绑定上原生事件。







