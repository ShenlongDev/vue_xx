<script setup>
import { ref } from 'vue'
import ButtonCounter from '@/components/ButtonCounter.vue'

const count = ref(0)
</script>

<template>
  <h1>组件基础</h1>
  <p>组件允许我们将 UI 划分为独立的、可重用的部分，并且可以对每个部分进行单独的思考。</p>
  <p>在实际应用中，组件常常被组织成一个层层嵌套的树状结构：</p>
  <p>这和我们嵌套HTML元素的方式类似，Vue实现了自己的组件模型，是我们可以在每个组件内封装自定义内容与逻辑。</p>
  <p>Vue同样也能很好地配合原生 Web Component。</p>
  <p>如果你想知道 Vue 组件与原生 Web Components 之间的关系，可以阅读此章节。</p>

  <h2>定义一个组件</h2>
  <p>当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 .vue 文件中，这被叫做单文件组件（简称 SFC）：</p>

  <button @click="count++">You clicked me {{ count }} times.</button>
  <h2>使用组件</h2>
  <p>要使用一个组件，我们需要在父组件中导入它。</p>
  <p>假设我们把计数器组件放在了一个叫做 ButtonCounter.vue 的文件中，这个组件将会默认导出的形式被暴露给外部。</p>

  <ButtonCounter />

  <p>通过 script setup，导入的组件都在模板中直接可用。</p>
  <p>当然你可以全局地注册一个组件，使得它在当前应用中的任何组件上都可以使用，而不需要额外再导入。</p>
  <p>关于组件的全局注册和局部注册两种方式的利弊，我们放在了组件注册这一章节中专门讨论。</p>
  <p>组件可以被宠用任意多次。</p>

  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />
</template>
