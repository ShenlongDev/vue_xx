<template>
  <h1>组件基础</h1>
  <h2>DOM 内模板解析注意事项</h2>
  <p>如果你想在 DOM 中直接书写 Vue 模板，Vue 则必须从 DOM 中获取模板字符串。</p>
  <p>由于浏览器的原生 HTML 解析行为限制，有一些需要注意的事项。</p>

  <h3>大小写区分</h3>
  <p>
    HTML 标签和属性名称是部分大小写的，所以浏览器会把任何大写的字符串解析为小写的。
    这意味着当你使用 DOM 内的模板时，无论是 PascalCase 形式的组件名称，camelCase 形式的 prop 名称
    还是 v-on 的事件名称，都需要转换为相应等价的 kebab-case （短横线链字符）形式：
  </p>
  <!-- HTML 中的 kebab-case -->
  <blog-post post-title="hello!" @update-post="onUpdatePost"></blog-post>
</template>

<script setup>
// JavaScript 中的 camelCase
const BlogPost = {
  props: ['postTitle'],
  emits: ['updatePost'],
  template: `
    <h3>{{ postTitle }}</h3>
  `
}
</script>
