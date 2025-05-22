<script setup>
import { ref, reactive } from 'vue'

const books = reactive([ref('Vue 3 Guide')])
// 这里需要 .value
console.log(books[0].value)

const map = reactive(new Map([['count', ref(0)]]))
// 这里需要 .value
console.log(map.get('count').value)
</script>

<template>
  额外的ref解包细节
  <h1>作为reactive对象的属性</h1>
  <p>一个ref会在作为响应式对象的属性被访问或修改时自动解包。和换句话说，他的行为就像一个普通的属性：</p>

  <p>如果将一个新的ref赋值给一个关联了已有ref的属性，那么他会替换掉旧的ref：</p>

  <h1>数组和集合的注意事项</h1>
  <p>与reactive对象不同的是，当ref作为响应式数组或原生集合类型（如Map）中的元素被访问时，他不会被解包</p>

  <h1>在模板中解包的注意事项</h1>
  <p>在模板中渲染上下文中，只有顶级的ref属性才会被解包。</p>
  在下面的例子中，count和object时顶级属性，但object.id不是：
  渲染的结果时，为了解决这个问题，我们可以将id结构为一个顶级属性：、现在渲染的结果将是2
  另一个需要注意的点是，如果ref是文本插值的最终计算值
  该特性仅仅是文本插值的一个便利特性，等价于 {{ object.id.value }}。
</template>

<style scoped></style>
