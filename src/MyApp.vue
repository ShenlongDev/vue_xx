<script setup>
import { reactive } from 'vue'

const state = reactive({ count: 0 })
const raw = {}
const proxy = reactive(raw)

console.log(proxy === raw)
</script>

<template>
  <button @click="state.count++">
    {{ state.count }}
  </button>

  还有另一种声明响应式状态的方式，及使用reactive()API。
  与将内布置包装在特殊对象中的ref不同，reactive()将使对象本身具有响应性。
  响应式对象是JS代理，其行为就和普通对象一样。
  不同的是Vue能够拦截对响应式对象所有属性的访问和修改，一遍进行以来追踪和触发更新。
  reactive() 将深层地转换对象：当访问嵌套对象时，它们也会被 reactive() 包装。当 ref 的值是一个对象时，ref() 也会在内部调用它。与浅层 ref 类似，这里也有一个 shallowReactive() API 可以选择退出深层响应性。

  Reactive Proxy vs. Original
  值得注意的是，reactive()返回的是一个原始对象的Proxy，他和原始对象是不相等的：
  只有代理有响应式的，更改原始对象不会触发更新。因此，使用Vue的响应式系统的最佳实践是仅使用你声明对象的代理版本。
  为保证访问代理的一致性，对不同一个原始对象调用reactive（）会总是返回同样的代理对象， 嗯对一个以已存在的代理对象调用reactive（）
  会返回其本身。

  reactive()局限性
  1.有限的值类型：它只能用于对象类型（对象，数组和如Map，Set这样的集合类型）。
  他不能持有如string，Boolean或number这样的原始类型
  2. 不能替换整个对象：由于Vue的响应式跟踪是通过属性访问实现的，因此我们必须始终保持对象影视对象的相同引用，
  这意味着我们不能轻易地‘替换’响应式对象，因为这样的话与第一个应用的响应性链接将丢失；
  对结构操作不友好：
  当我们将响应式对象的原始类型属性结构为本地变量时，或者将该属性传递函数时，我们将丢失响应性链接：
</template>

<style scoped></style>
