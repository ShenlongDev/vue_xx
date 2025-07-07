<script setup>
import { ref } from 'vue'

const text = ref('')
const message = ref('')
const checkedNames = ref([])
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

  <h2>基本用法</h2>
  <h3>文本</h3>
  <p>Message is: {{ message }}</p>
  <input v-model="message" placeholder="edit me" />
  <h3>多行文本</h3>
  <span>Multiline message is:</span>
  <p style="white-space: pre-line;">{{ message }}</p>
  <textarea v-model="message" placeholder="add multiple lines"></textarea>
  <p>注意在 textarea 中是不支持插值表达式的。请使用 v-model 来替代：</p>
  <!-- 错误 -->
  <textarea>{{ text }}</textarea>
  <!-- 正确 -->
  <textarea v-model="text"></textarea>
  <h3>复选框</h3>
  <p>单一的复选框，绑定布尔类型值：</p>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>
  <p>我们也可以将多个复选框绑定到同一个数组或集合的值：</p>
  <div>Checked names: {{ checkedNames }}</div>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <p>在这个例子中，checkedNames 数组将始终包含所有当前被选中的框的值。</p>
  <h3>单选按钮</h3>
  <div>Picked: {{ picked }}</div>
  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">One</label>
  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
</template>
