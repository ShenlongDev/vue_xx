<template>
  <h1>生命周期钓子</h1>
  <p>
    每个 Vue 组件实例在创建时都需要经历一系列的初始化步骤，比如设置好数据侦听，编译模板，挂载实例到 DOM，以及在数据改变时更新 DOM。
    在此过程中，它也会运行被称为生命周期钩子的函数，让开发者有机会在特定阶段运行自己的代码。
  </p>

  <h2>注册周期钩子</h2>
  <p>
    举例来说，onMounted 钩子可以用来在组件完成初始渲染并创建 DOM 节点后运行代码：
    还有其他一些钩子，会在实例生命周期的不同阶段被调用，最常用的是 onMounted、onUpdated 和 onUnmounted。所有生命周期钩子的完整参考及其用法请参考 API 索引。

    当调用 onMounted 时，Vue 会自动将回调函数注册到当前正被初始化的组件实例上。这意味着这些钩子应当在组件初始化时被同步注册。例如，请不要这样做：

    注意这并不意味着对 onMounted 的调用必须放在 setup() 或 script setup 内的词法上下文中。onMounted() 也可以在一个外部函数中调用，只要调用栈是同步的，且最终起源自 setup() 就可以。
  </p>
</template>


<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  console.log(`the component is now mounted.`)
})

setTimeout(() => {
  onMounted(() => {
    // 异步注册时当前组件实例已丢失
    // 这将不会正常工作
  })
}, 100)
</script>
