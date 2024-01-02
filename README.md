# front-end-interview

## vue

### 生命周期和钩子函数

vue 中每一个组件都有自己的生命周期，会经过组件创建、数据初始化、挂载、更新、销毁等过程，在这个过程中会运行生命周期钩子函数，这使得用户有机会添加自己的代码，生命周期可以分为 8 个阶段：创建前后、挂载前后、更新前后、销毁前后。

| vue2          | vue3            | 调用时机          |
| ------------- | --------------- | ----------------- |
|               | setup           | 最开始            |
| beforeCreate  |                 | 组件实例初始化前  |
| created       |                 | 组件实例创建后    |
| beforeMount   | onBeforeMount   | 组件挂载到 DOM 前 |
| mounted       | onMounted       | 组件挂载到 DOM 后 |
| beforeUpdate  | onBeforeUpdate  | 组件更新前        |
| updated       | onUpdated       | 组件更新后        |
| beforeDestroy | onBeforeUnmount | 组件卸载前        |
| destroyed     | onUnmounted     | 组件卸载后        |

### 双向绑定原理

vue2 是通过**数据劫持**的方式，使用 Object.defineProperty() 实现的

vue3 是通过**数据代理**的方式，使用 es6 中的 Proxy 实现的

区别：

- vue2 中是对对象的所有属性进行递归。而 vue3 是按需递归，性能更高。
- vue2 中对象不存在的属性是不能被拦截的。而 vue3 可以，功能更强大。

### 路由守卫

全局路由守卫：

- beforeEach: 全局前置路由守卫，每次路由切换之前被调用

- beforeResolve：全局解析守卫，在导航被确认之前、所有组件内守卫和异步路由组件被解析之后调用

- afterEach: 全局后置路由守卫，每次路由切换之后调用

路由独享守卫：

- beforeEnter: 独享前置路由守卫，只对单个路由配置

组件路由守卫：

- beforeRouteEnter: 通过路由规则进入该组件时被调用

- beforeRouteUpdate：当前路由改变是被调用

- beforeRouteLeave: 通过路由规则离开该组件时被调用
