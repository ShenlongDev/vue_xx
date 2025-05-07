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

  // 这里导入，声明的变量和函数可在同一组件的模板中直接使用。
  // 你可以理解为模板是在同意作用域内声明一个JS函数，它自然可以访问与它一起设革命的所有内容。
</script>

<template>
  # 响应式基础
  # script setup
  在setup函数中手动暴露大量的状态和方法非常繁琐。
  幸运的是，我们可以使用通过单文件组件的来避免这种情况的。
  我们可以使用《script setup》来大幅度地简化代码
</template>

<style scoped>
  
</style>
