<script setup>
import { ref } from 'vue'
const isActive = ref(true)
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定 HTML class</h2>
  <h3>在组件上使用</h3>
  <p>本届假设你已经有Vue组件的知识基础。如果没有，你也可以暂时跳过，以后再阅读</p>
  对于只有一个根元素的组件，当你使用了class sttribute时，这些class会被添加到跟元素上并与该元素上已有的class合并。
  举例来说，如果你生命了一个组件名叫MyComponent，模板如下：
  <!-- 字组件模板 -->
  <p class="foo bar">Hi!</p>
  在使用时添加一些class：
  <!-- 在使用组件时 -->
  <MyComponent class="baz boo" />

  渲染的HTML为：
  <p class="foo bar baz boo">这是被渲染的HTML</p>

  Class的绑定也是同样的：
  <MyComponent :class="{ active: isActive }" />

  当isActive为真时，被渲染的HTML会是：
  <p class="foo bar active">Hi!</p>

  如果你的组件有多个根元素，你将需要指定那个根元素来接受这个class。
  你可以通过组件的 $attrs属性来指定接受的元素：

  <!-- MyComponent 模板使用 $attrs 时 -->
  <p :class="$attrs.class">Hi!</p>
  <span>This is a child component</span>
  <MyComponent class="baz" />

  这将被渲染为：
  <p class="baz">Hi!</p>
  <span>This is a child component</span>

  你可以在透传Attribute一章中了解更多组件的attribute继承的细节
</template>

<style scoped></style>
