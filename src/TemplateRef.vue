<script setup>
import { useTemplateRef, onMounted, watchEffect } from 'vue';
import Child from './components/ChildRef.vue'

// 第一个参数必须与模板中的 ref 值匹配
const input = useTemplateRef('my-input')

onMounted(() => {
  input.value.focus()
})

watchEffect(() => {
  if (input.value) {
    input.value.focus()
  } else {
    // 此时还未挂载，或此元素已经被卸载（例如通过 v-if 控制）
  }
})

const ChildRef = useTemplateRef('child')

onMounted(() => {
  console.log(ChildRef.value)
})

import { ref } from 'vue'
const a = 1
const b = ref(2)

// 像 defineExpose 这样的编译器宏不需要导入
defineExpose({
  a,
  b
})

const list = ref([
  1, 2, 3, 4, 5
])

// const itemRefs = useTemplateRef('items')
// onMounted(() => console.log(itemRefs.value))
const itemRefs = ref([])

onMounted(() => console.log(itemRefs.value))
</script>

<template>
  <h1>模板引用</h1>
  虽然 Vue 的声明性渲染模型为你抽象了大部分对 DOM 的直接操作，
  但在某些情况下，我们仍然需要直接访问底层 DOM 元素。
  要实现这一点，我们可以使用特殊的 ref 属性：
  <input ref="input">
  ref 是一个特殊的 attribute，和 v-for 章节中提到的 key 类似。
  它允许我们在一个特定的 DOM 元素或子组件实例被挂载后，获得对他的直接引用。
  这可能很有用，比如说在组件挂载时将焦点设置一个 input 元素上，或在一个元素上初始化一个第三方库。

  <h2>访问模板引用</h2>
  要在组合式 API 中获取引用，我们可以使用辅助函数 useTemplateRef():
  <input ref="my-input">
  在使用 TypeScript 时，Vue 的 IDE 支持和 vue-tsc 将根据匹配的 ref attribute 所用的元素或组件自动推断 input.value 的类型。
  —— 3.5以前的用法
  注意，你只可以在组件挂载后才能访问模板引用。
  如果你想在模板中的表达式上访问 input，你初次渲染时会是 null。
  这是因为在初次渲染前这个元素还不存在呢！
  如果你需要侦听一个模板引用 ref 的变化，确保考虑到其值为 null 的情况：
  也可参考：为模板引用标注类型

  <h2>组件上的 ref</h2>
  这一小节假设你已了解组件的相关知识，或者你也可以先跳过这里，之后在回来看。
  模板引用也可以被用在一个子组件上。
  这种情况下引用中获得的值是组件实例：
  <Child ref="child" />
  —— 3.5 前的用法
  如果一个子组件使用的是选项式 API 或没有使用 script setup,
  被引用的组件实例和该子组件的 this 完全一致，
  这意味着父组件对子组件的每一个属性和方法都有完全的访问权。
  这使得在父组件和子组件之间创建紧密耦合的实现细节变得很容易，
  当然也因此，应该只在绝对需要时才使用组件引用。
  大多数情况下，你应该首先使用标准的 props 和 emit 接口来实现父子组件交互。
  有一个例外的情况，使用了 script setup 的组件是默认私有的：
  一个父组件无法访问到一个使用了 script setup 的子组件中的任何东西，
  除非子组件在其中通过 defineExpose 宏显式暴露：
  当父组件通过模板引用获取到了该组件的实例时，得到的实例类型为 { a: number, b: number } (ref 都会自动解包，和一般的实例一样)。
  请注意，defineExpose 必须在任何 await 操作之前调用。
  否则，在 await 操作后暴露的属性和方法将无法访问。
  TypeScript 用户请参考：为组件的模板引用标注类型

  <h2>v-for 中的模板引用</h2>
  挡在 v-for 中使用模板引用时，对应的 ref 中包含的值是一个数组，
  他将在元素被挂载后包含对应整个列表的所有元素：
  <ul>
    <li v-for="item in list" :key="item" ref="items">
      {{ item }}
    </li>
  </ul>
  —— 3.5前的用法
  在 3.5 版本以前，useTemplateRef() 尚未引入，需要声明一个与模板引用 attribute 同名的 ref。
  该 ref 的值需要是一个数组。
  应该注意的是，ref 数组并不保证与源数组相同的顺序。

  <h2>函数模板引用</h2>
  除了使用字符串值作名字，ref attribute 还可以绑定为一个函数，会在每次组件更新时都被调用。
  该函数会收到元素引用作为其第一个参数：
  <input :ref="(el) => { /* 将 el 赋值给一个数据属性或 ref 变量 */ }">
  注意我们这里需要使用动态的 :ref 绑定才能够传入一个函数。
  当绑定的元素被卸载时，函数也会被调用一次，此时的 el 参数会是 null。
  你当然也可以绑定一个组件方法而不是内联函数。
</template>
