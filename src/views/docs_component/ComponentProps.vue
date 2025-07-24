<template>
  <h1>Props</h1>
  <h2>Props 声明</h2>
  <p>一个组件需要显式声明它所接受的 props，这样 Vue 才能知道外部传入的哪些是 props，哪些是透传 attribute。</p>
  <p>在使用 script setup 的单文件组件中，props可以使用 defineProps() 宏来声明。</p>
  <p>在没有使用 script setup 的组件中，props 可以用 props 选项来声明：</p>
</template>

<!-- <script setup>
const props = defineProps(['foo'])

console.log(props.foo)
</script> -->
<script>
export default {
  props: ['foo'],
  setup(props) {
    console.log(props.foo)
  }
}
</script>
