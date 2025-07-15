<script setup>
</script>


<template>
  <h1>组件基础</h1>
  <h2>传递 Props</h2>
  <p>
    如果我们正在构建一个博客，我们可能需要一个博客文章的组件。
    我们希望所有的博客文章分享相同的视觉布局，但不同的内容。
    要实现这样的效果自然必须想组件中传递数据，例如每篇文章标题和内容，这就会使用到 Props。
  </p>
  <p>
    Props 是一种特别的 attributes，你可以在组件上声明注册。
    要传递给博客文章组件一个标题，我们必须在组件的 props 列表上声明它。
    这里要用到 defineProps 宏：
  </p>
  <p>
    defineProps 是一个仅 script setup 中可用的编译宏命令，并不需要显式地导入。
    声明的 Props 会自动暴露给模板。
    defineProps 会返回一个对象，其中包含了可以传递给组件的所有 props：
  </p>
  <p>
    TypeScript 用户请参考：为组件 props 标注类型
  </p>
</template>
