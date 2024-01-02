# front-end-interview

## vue

### 生命周期和钩子函数

vue 中每一个组件都有自己的生命周期，会经过组件创建、数据初始化、挂载、更新、销毁等过程，在这个过程中会运行生命周期钩子函数，这使得用户有机会添加自己的代码，生命周期可以分为8个阶段：创建前后、挂载前后、更新前后、销毁前后。

| vue2          | vue3            | 调用时机
| -             | -               | -
|               | setup           | 最开始
| beforeCreate  |                 | 组件实例初始化前
| created       |                 | 组件实例创建后
| beforeMount   | onBeforeMount   | 组件挂载到DOM前
| mounted       | onMounted       | 组件挂载到DOM后
| beforeUpdate  | onBeforeUpdate  | 组件更新前
| updated       | onUpdated       | 组件更新后
| beforeDestroy | onBeforeUnmount | 组件卸载前
| destroyed     | onUnmounted     | 组件卸载后
