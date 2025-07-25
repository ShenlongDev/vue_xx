<template>
  <h1>Props</h1>
  <h2>传递 prop 的细节</h2>
  <h3>Prop 名字格式</h3>
  <p>如果一个 prop 的名字很长，应使用 camelCase 形式，因为它们是合法的 JavaScript 标识符，可以直接在模板的表达式中使用，也可以避免在作为属性 key 名时必须加上引号。</p>
  <span>{{ greetingMessage }}</span>
  <p>虽然理论上你也可以在向子组件传递 props 时使用 camelCase 形式，但实际上为了和 HTML attribute 对齐，我们通常会将其写为 kebab-case 的形式：</p>
  <MyComponent greeting-message="hello" />
  <p>对组件名我们推荐使用 PascalCase，因为这提高了模板可读性，能帮助我们区分 Vue 组件和原生 HTML 元素。然而对于传递 props 来说，使用 camelCase 并没有太多的优势，因此我们推荐更贴近 HTML 的书写风格。</p>
</template>

<script setup>
const props = defineProps({
  greetingMessage: String
})

// 定义子组件
const MyComponent = {
  props: {
    greetingMessage: String
  },
  template: `<span>hello, {{ greetingMessage }}</span>`
}
</script>
