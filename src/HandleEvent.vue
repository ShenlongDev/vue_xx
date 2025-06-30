<script setup>
import { ref } from 'vue'

const cnt = ref(0)
const name = ref('Vue')

function greeting(event) {
  alert(`Hello, ${name.value}!`)

  if (event) {
    alert(event.target.tagName)
  }
}

function say(message) {
  alert(message)
}
</script>

<template>
  <h1>事件处理</h1>

  <h2>监听事件</h2>
  <p>
    我们可以使用 v-on 指令 (简写为 @) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。
    用法：v-on:click="handler" 或 @click="handler"。
    事件处理器 (handler) 的值可以是：
    <b>1.内联事件处理器</b>：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。
    <b>2.方法事件处理器</b>：一个指向组件上定义的方法的属性名或是路径。
  </p>

  <h2>内联事件处理器</h2>
  <button @click="cnt++">Add 1</button>
  <p>The button above has been clicked {{ cnt }} times.</p>

  <h2>方法事件处理器</h2>
  <p>随着事件处理器的逻辑变得愈发复杂，内联代码方式变得不够灵活。</p>
  <p>因此 v-on 也可以接受一个方法名或对某个方法调用。</p>
  <button @click="greeting">Greet</button>
  <p>方法事件处理器会自动接收原生 DOM 事件并触发执行。</p>
  <p>在上面的例子中，我们能够通过被触发事件的 event.target 访问到该 DOM 元素。</p>
  <p>你也可以看看为事件处理器标注类型这一章了解更多。</p>
  <h3>方法与内联事件判断</h3>
  <p>模板编译器会通过检查 v-on 的值是否是合法的 JavaScript 标识符或属性访问路径来断定是何种形式的事件处理器。</p>
  <p>举例来说，foo、foo.bar 和 foo['bar'] 会被视为方法事件处理器，而 foo() 和 count++ 会被视为内联事件处理器。</p>

  <h2>在内联处理器中调用方法</h2>
  <p>除了直接绑定方法名，你还可以在内联事件处理器中调用方法。</p>
  <p>这允许我们向方法传入自定义参数以代替原生事件：</p>
  <button @click="say('hello')">Say hello</button>
  <button @click="say('bye')">Say bye</button>
</template>
