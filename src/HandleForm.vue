<script setup>
import { ref } from 'vue'

const text = ref('')
</script>

<template>
  <h1>表单输入绑定</h1>

  <p>在前端处理表单时，我们常常需要将表单输入框的内容同步给 JavaScript 中相应的变量。</p>
  <p>手动连接值绑定和更改事件监听器可能会很麻烦：</p>
  <input
    :value="text"
    @input="event => text = event.target.value">
  <p>v-model 指令帮我们简化了这一步骤：</p>
  <input v-model="text">
  <p>另外， v-model 还可以用域各种不同类型的输入，textarea，select 元素。</p>
  <p>他会根据所使用的元素自动使用对应的 DOM 属性和事件组合：</p>
  <ol>
    <li>文本类型的 input 和 textarea 元素会绑定 value property 并侦听 input 事件；</li>
    <li>checkbox 和 radio 会绑定 checked property 并侦听 change 事件；</li>
    <li>select 会绑定 value property 并侦听 change 事件。</li>
  </ol>
</template>
