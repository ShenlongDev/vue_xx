<script setup>

</script>


<template>
  <h1>组件基础</h1>
  组件允许我们将 UI 发分为独立的，可重用的部分，并且可以对每个部分进行独立的思考。
  在实际应用中，组件常常被组织成一个层层嵌套的树状结构：
  这和我们嵌套 HTML 元素的方式类似，Vue 实现了自己的组件模型，是我们可以在每个组件内封装自定义内容与逻辑。
  Vue 同样也能很好地配合原生 Web Component。
  如果你想知道 Vue 组件与原生 Web Component之间的关系，可以阅读此章节。

  <h2>定义一个组件</h2>
  当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 .vue 文件中，这被叫做单文件组件（简称 SFC）：

  当不使用构建步骤时，一个 Vue 组件以一个包含 Vue 特定选项的 JavaScript 对象来定义：
  import { ref } from 'vue'

  export default {
    setup() {
      const count = ref(0)
      return { count }
    },
    template: `
      <button @click="count++">
        You clicked me {{ count }} times.
      </button>`
    // 也可以针对一个 DOM 内联模板：
    // template: '#my-template-element'
  }

  这里的模板时一个内联的 JavaScript 字符串， Vue 将会在运行时编译它。
  你也可以使用 ID 选择器来只想一个元素（通常是原生的 template 元素），Vue 将会使用其内容作为模板来源。

  上面的例子中定义了一个组件，并在一个 .js 文件里默认导出了它自己，但你也可以通过具名导出在一个文件中导出多个组件。
</template>
