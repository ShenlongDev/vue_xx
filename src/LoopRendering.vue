<script setup>
import CodeView from './components/CodeView.vue';
import HeadingTwo from './components/HeadingTwo.vue';
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
</template>
