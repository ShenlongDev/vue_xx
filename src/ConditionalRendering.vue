<script setup>
import { ref } from 'vue'
import CodeView from '@/components/CodeView.vue'
import HeadingTwo from './components/HeadingTwo.vue'

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

  <HeadingTwo heading="v-show" />
  <p>另一个可以用来按条件显示一个元素的指令是v-show</p>
  <CodeView :content="`<h1 v-show='ok'>Hello!</h1>`" />
  <p>不同之处在于v-show会在DOM渲染中保留该元素；</p>
  <p>v-show进切换了该元素上名为display的CSS属性</p>
  <p>v-show不支持在template元素上使用，也不能和v-else搭配使用</p>

  <HeadingTwo heading="v-if" />vs.<HeadingTwo heading="v-show" />
  <p>v-if是“真是”的按条件渲染，因为它确保了在切换时，条件区块内的时间监听器和子组件都会被销毁和重建。</p>
  <p>v-if也是惰性的：如果在初次渲染时条件值为false，则不会做任何事。</p>
  <p>条件区块只有当条件手持变为true时才被渲染。</p>
  <p>相比之下，v-show简单许多，元素无论初始条件如何，始终会被渲染，只有CSS display属性会被切换。</p>
  <p>总的来说，v-if有更高的切换开销，而v-show有更高的初始渲染开销。</p>
  <p>因此，如果需要频繁切换在，则使用v-show较好；如果在运行时绑定条件很少改变，则v-if会更合适。</p>
</template>

<style></style>
