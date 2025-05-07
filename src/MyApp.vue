<script setup>
  import { ref } from 'vue'

  const cnt = ref(0)

  console.log(cnt)
  console.log(cnt.value)

  cnt.value++
  console.log(cnt)
  console.log(cnt.value)

  const increment = () => {
    cnt++
  }
</script>

<template>
  # 响应式基础
  # 声明响应式状态
  ref()
  在组合式API中，推荐使用ref()函数来声明响应式状态：

  ref() 接受参数，并将其包裹在带有.value属性的对象中返回：
  <div>这是REF的实例</div>
  <button @click="increment">我是 {{ cnt }} 遍按下的</button>

  要在模板中访问ref，请从组件的setup()函数中声明并返回它们：
  注意：在模板中使用ref时，我们不需要附加.value。
  为了方便起见，挡在模板中使用时，ref会自动解包。
  你可以在事件监听器中改变一个ref:

  对于更复杂的逻辑，我们可以在同意作用域内声明更改ref的函数，并将他们作为方法与状态一起公开
  然后，暴露的方法剋以用作时间监听器

  这里是Codepen上的例子，没有使用任何构建工具。
</template>

<style scoped>
  
</style>
