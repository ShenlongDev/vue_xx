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

  // 伪代码，不是真正的实现
  const myRef = {
    _value: 0,
    get value() {
      track()
      return this._value
    },
    set value(newValue) {
      this._value = newValue
      trigger()
    }
  }

  // 这里导入，声明的变量和函数可在同一组件的模板中直接使用。
  // 你可以理解为模板是在同意作用域内声明一个JS函数，它自然可以访问与它一起设革命的所有内容。
</script>

<template>
  你可能会好奇：为什么我们需要使用带有 .value 的 ref，而不是普通的变量？为了解释这一点，我们需要简单地讨论一下 Vue 的响应式系统是如何工作的。

  当你在模板中使用了一个 ref，然后改变了这个 ref 的值时，Vue 会自动检测到这个变化，并且相应地更新 DOM。这是通过一个基于依赖追踪的响应式系统实现的。当一个组件首次渲染时，Vue 会追踪在渲染过程中使用的每一个 ref。然后，当一个 ref 被修改时，它会触发追踪它的组件的一次重新渲染。

  在标准的 JavaScript 中，检测普通变量的访问或修改是行不通的。然而，我们可以通过 getter 和 setter 方法来拦截对象属性的 get 和 set 操作。

  该 .value 属性给予了 Vue 一个机会来检测 ref 何时被访问或修改。在其内部，Vue 在它的 getter 中执行追踪，在它的 setter 中执行触发。从概念上讲，你可以将 ref 看作是一个像这样的对象：

</template>

<style scoped>
  
</style>
