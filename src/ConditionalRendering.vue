<script setup>
import { ref } from 'vue'
import CodeView from '@/components/CodeView.vue'

const awesome = ref(true)

const vElseStr = `<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>`

const vElseIfStr = `<div v-if="type === 'A'">
  A
</div>
<div v-else-if="type === 'B'">
  B
</div>
<div v-else-if="type === 'C'">
  C
</div>
<div v-else>
  Not A/B/C
</div>`

const templateVIfStr = `<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>`
</script>

<template>
  <h1>条件渲染</h1>
  <h2>v-if</h2>
  <p>v-if 指令用域条件性地渲染一块内容。</p>
  <p>这块内容只会在指令的表达式返回真时才被渲染。</p>
  <CodeView content="<h1 v-if='awesome'>Vue is awesome!</h1>" />
  <h1 v-if="awesome">Vue is awesome!</h1>

  <h2>v-else</h2>
  <p>你也可以使用v-else为v-if添加一个“else区块”</p>
  <CodeView :content="vElseStr" />

  <button @click="awesome = !awesome">Toggle</button>

  <h1 v-if="awesome">Vue is awesome!</h1>
  <h1 v-else>Oh no 😢</h1>

  <p>一个v-else元素必须跟在一个v-if或者v-else-if元素后面，否则它将不会被识别。</p>

  <h2>v-else-if</h2>
  <p>顾名思义，v-else-if 提供的时相应于v-if的“else-if区块”。</p>
  <p>它可以连续多次重复使用。</p>
  <CodeView :content="vElseIfStr" />

  <p>和v-else类似，一个使用v-else-if的元素必须紧跟在一个v-if或一个v-else-if元素后面。</p>

  <h2>template上的v-if</h2>
  <p>因为v-if是一个指令，他必须依附于某个元素。</p>
  <p>但如果我们想要切换不止一个元素呢？</p>
  <p>在射中情况下我们可以在一个template元素上使用v-if，这只是不可兼得包装器元素，最后渲染的结果并不会包含这个teamplate元素。</p>
  <CodeView :content="templateVIfStr" />

  <p>v-else和v-else-if也可以在template上使用。</p>
</template>

<style></style>
