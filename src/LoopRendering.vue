<script setup>
import CodeView from './components/CodeView.vue';
import HeadingTwo from './components/HeadingTwo.vue';
import EnLetter from './components/EnLetter.vue';

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
</template>
