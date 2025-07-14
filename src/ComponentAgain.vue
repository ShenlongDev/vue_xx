<script setup>
import CounterComponent from './components/CounterComponent.vue'
</script>


<template>
  <h1>组件基础</h1>
  <h2>使用组件</h2>
  要使用一个子组件，我们需要在父组件中导入它。
  假设我们把计数器组件放在了一个叫做 `CounterComponent.vue` 的文件中，这个组件将会以默认导出的形式被暴露给外部。
  <CounterComponent />
  通过 script setup 导入的组件都在模板中直接可用。
  当然，你也可以全局地注册一个组件，使得他在当前应用中的任何组件上都可以使用，而不需要额外在导入。
  关于组件的全局注册和局部注册两种方式的利弊，我们放在了组件注册这一章节中专门讨论。
  组件可以被重用任意多次：
  <h3>Here is a child component!</h3>
  <CounterComponent />
  <CounterComponent />
  <CounterComponent />
  <p>
    你会注意到，每当点击这些按钮时，每一个组件都维护者自己的状态，是不同的 count。
    这是因为每当你使用一个组件，就创建的一个新的实例。
    在单文件组件中，推荐为子组件使用 PascalCase 标签名，以此来原生的 HTML 元素做区分。
    虽然原生 HTML 标签名时不区分大小写的，但 Vue 单文件组件时可以在编译中区分大小写的。
    我们也可以使用 /> 来关闭一个标签。
    如果你是直接在 DOM 中书写模板，（例如原生 template 元素的内容），模板的编译需要遵从浏览器中 HTML 的解析行为。
    在这种情况下，你应该需要使用 kebab-case 形式并显式地关闭这些组件的标签。
  </p>
  <counter-component></counter-component>
  <counter-component></counter-component>
  <counter-component></counter-component>
  <p>
    请看 DOM 内模板解析注意事项了解更多细节。
  </p>
</template>
