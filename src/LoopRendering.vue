<script setup>
import CodeView from './components/CodeView.vue';
import HeadingTwo from './components/HeadingTwo.vue';
import EnLetter from './components/EnLetter.vue';
import { computed } from 'vue';

const parentMessage = 'Parent'
const items = [
  /* ... */
]

items.forEach((item, index) => {
  // 可以访问外层的 `parentMessage`
  // 而 `item` 和 `index` 只在这个作用域可用
  console.log(parentMessage, item.message, index)
})
</script>

<template>
  <h1>列表渲染</h1>
  <HeadingTwo heading="v-for" />
  <p>我们可以使用v-for指令基于一个数组来渲染一个列表。</p>
  <p>v-for指令的值需要使用 item in items 形式的特殊语法，其中 items 是元数据的数组，而 item 是迭代项目的别名：</p>
  <CodeView :content="`const items = ref([{ message: 'Foo' }, { message: 'Bar' }])`" />
  <CodeView :content='`<li v-for="item in items">
  {{ item.message }}
</li>`' />

  <p>在
    <EnLetter content="v-for" /> 块中可以完整地访问父作用域内的属性和变量。
    <EnLetter content="v-for" />也支持使用可选的第二个参数表示当前想的位置索引。
  </p>

  <CodeView :content="`const parentMessage = ref('Parent')
const items = ref([{ message: 'Foo' }, { message: 'Bar' }])`" />
  <CodeView :content='`<li v-for="(item, index) in items">
  {{ parentMessage }} - {{ index }} - {{ item.message }}
</li>`' />

  <p>
    <EnLetter content="v-for" />变量的作用域和下面的 JavaScript 代码是很类似：
  </p>
  <CodeView :content="`const parentMessage = 'Parent'
const items = [
  /* ... */
]

items.forEach((item, index) => {
  // 可以访问外层的 'parentMessage'
  // 而 'item' 和 'index' 只在这个作用域可用
  console.log(parentMessage, item.message, index)
})`" />

  <p>注意 <EnLetter content="v-for" />是如何对应<EnLetter content="forEach" />回调的函数签名的。
    实际上，你也可以在定义 <EnLetter content="v-for" />的变量别名时使用结构，和结构函数参数类似：</p>
  <CodeView :content='`<li v-for="{ message } in items">
  {{ message }}
</li>

<!-- 有 index 索引时 -->
<li v-for="({ message }, index) in items">
  {{ message }} {{ index }}
</li>`' />

<p>对于多层嵌套的<EnLetter content="v-for" />,作用域的工作方式和函数的作用域很类似。
每个<EnLetter content="v-for" />作用域都可以访问到父级作用域：</p>

<CodeView :content='`<li v-for="item in items">
  <span v-for="childItem in item.children">
    {{ item.message }} {{ childItem }}
  </span>
</li>`' />
<p>你也可以使用<EnLetter content="of" />作为分隔符来替代<EnLetter content="in" />这更接近 JavaScript 的迭代器语法：</p>
<CodeView :content='`<div v-for="item of items"></div>`' />

<HeadingTwo heading="v-for与对象" />

<p>你也可以使用<EnLetter content="v-for" />来遍历一个对象的所有属性。便利的顺序会给予对该对象调用<EnLetter content="Object.values()" />的返回值来决定。</p>
<CodeView :content="`const myObject = reactive({
  title: 'How to do lists in Vue',
  author: 'Jane Doe',
  publishedAt: '2016-04-10'
})`" />
<CodeView :content='`<ul>
  <li v-for="value in myObject">
    {{ value }}
  </li>
</ul>`' />

<p>可以通过提供第二个参数表示属性名(例如key:)</p>
<CodeView :content='`<li v-for="(value, key) in myObject">
  {{ key }}: {{ value }}
</li>`' />

<p>第三个参数表示位置索引：</p>
<CodeView :content='`<li v-for="(value, key, index) in myObject">
  {{ index }}. {{ key }}: {{ value }}
</li>`' />

<HeadingTwo heading="在 v-for 里使用范围值" />
<p><EnLetter content="v-for" />可以直接接受一个整数值。在值中用例中，会将该模板给予<EnLetter content="1...n" />的取值范围重复多次。</p>

<CodeView :content='`<span v-for="n in 10">{{ n }}</span>`' />
<p>注意此处 <EnLetter content="n" />的初值时从<EnLetter content="1" />开始而非<EnLetter content="0" />。</p>

<HeadingTwo heading="<template> 上的 v-for" />
<p>与模板上的 v-if 类似，你也可以在 <EnLetter content="<template>" /> 标签上使用 v-for 来渲染一个包含多个元素的块。例如：</p>
<CodeView :content='`<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>`' />

<HeadingTwo heading="v-for 与 v-if" />
<p>当他们同时存在于一个节点上时，v-if比v-for的优先级更高。这意味着v-if的条件将无法访问到v-for作用域内定义的变量的别名。</p>
<CodeView :content='`<!--
 这会抛出一个错误，因为属性 todo 此时
 没有在该实例上定义
-->
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo.name }}
</li>`' />
<p>在外先包装一层<EnLetter content="<template>" />再在其上使用<EnLetter content="v-for" />可以解决这个问题（这也更加明显易读）。</p>
<CodeView :content='`<template v-for="todo in todos">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>`' />

<HeadingTwo heading="通过key管理状态" />
<p>Vue默认按照”就地更新“的策略来更新通过 v-for 渲染的元素列表。当数据顶的顺序改变时，Vue不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保他们在原本是定的索引位置上渲染。</p>
<p>默认模式是高效的，但只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况。</p>
<p>为了给 Vue 一个提示，以便它可以跟踪每个节点的标识，从而重用和重新排序现有的元素，你需要为每个元素对应的块提供一个唯一的 key attribute：</p>
<CodeView :content='`<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>`' />
<p>当你使用 <EnLetter content="<template v-for>" /> 时，key 应该被放置在这个 <EnLetter content="<template>" /> 容器上：</p>
<CodeView :content='`当你使用 <template v-for> 时，key 应该被放置在这个 <template> 容器上：`' />
  <p>推荐在任何可行的时候为 v-for 提供一个 key attribute，除非所迭代的 DOM 内容非常简单 (例如：不包含组件或有状态的 DOM 元素)，或者你想有意采用默认行为来提高性能。</p>
  <p>key 绑定的值期望是一个基础类型的值，例如字符串或 number 类型。不要用对象作为 v-for 的 key。关于 key attribute 的更多用途细节，请参阅 key API 文档。</p>

<HeadingTwo heading="组件上使用 v-for" />
<p>我们可以直接在组件上使用 v-for，和在一般的元素上使用没有区别 (别忘记提供一个 key)：</p>
<CodeView :content='`<MyComponent v-for="item in items" :key="item.id" />`' />
<p>但是，这不会自动将任何数据传递给组件，因为组件有自己独立的作用域。为了将迭代后的数据传递到组件中，我们还需要传递 props：</p>
<CodeView :content='`<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>`' />
<p>不自动将 item 注入组件的原因是，这会使组件与 v-for 的工作方式紧密耦合。明确其数据的来源可以使组件在其他情况下重用。</p>
<p>这里是一个简单的 Todo List 的例子，展示了如何通过 v-for 来渲染一个组件列表，并向每个实例中传入不同的数据。</p>

<HeadingTwo heading="数组变化侦测" />
<h5>变更方法</h5>
<p>Vue能够侦听响应式数组的变更方法，并在他们被调用时触发相关的更新。这些变更方法包括：</p>
<CodeView :content='`push()、pop()、shift()、unshift()、splice()、sort()、reverse()`' />
<h5>替换一个数组</h5>
<p>变更方法，顾名思义，就是会对调用他们的原数组进行变更。相对地，也有一些不可变方法，例如 filter(), concat(), slice()
  这些都不会更改原数组，而说时返回一个新数组。当遇到的是非变更方法时，我们需要将旧的数组替换为新的：
</p>
<CodeView :content='`// items 是一个数组的 ref
items.value = items.value.filter((item) => item.message.match(/Foo/))`' />
<p>你可能认为这将导致 Vue 丢弃现有的 DOM 并重新渲染整个列表——幸运的是，情况并非如此。Vue 实现了一些巧妙的方法来最大化对 DOM 元素的重用，因此用另一个包含部分重叠对象的数组来做替换，仍会是一种非常高效的操作。</p>
</template>
