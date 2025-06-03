<script setup>
import { ref, computed } from 'vue'
const isActive = ref(true)
const hasError = ref(false)

const error = ref(null)

const classObject = computed(() => ({
  active: isActive.value && !error.value,
  'text-danger': error.value && error.value.type === 'fatal'
}))
</script>

<template>
  <h1>类与样式绑定</h1>
  <h2>绑定 HTML class</h2>
  <h3>绑定对象</h3>
  <p>我们可以给 :class (v-bind:class 的缩写) 传递一个对象来动态切换 class：</p>
  <div class="static" :class="{ active: isActive, 'text-danger': hasError }">
    <p>这里的语法表示active是否存在取决于数据属性isActive的真假值。</p>
    <p>你可以在对象中写多个字段来操作多个class。</p>
    <p>此外，：class指令也可以和一般的 class attribute共存。</p>
    <p>举例来说,下面这样的状态：</p>
    <p>配合一下模板</p>
    <div class="static" :class="{ active: isActive, 'text-danger': hasError }"></div>
    <p>渲染的结果会是：</p>
    <div class="static active">当isActive或者hasError改变时，class列表会随之更新</div>
    <p>举例来说，如果hasError变为true，class列表会变成“static active text-danger”。</p>
    <p>绑定的对象并不一定需要写成内敛字面量的形式，也可以直接绑定一个对象：</p>

    <div :class="classObject"></div>

    这将渲染：
    <div class="active"></div>

    我们也可以绑定一个返回对象的计算属性。这是一个常见且很有用的技巧：

    <div :class="classObject"></div>
  </div>
</template>

<style scoped></style>
