<script>
import { ref } from 'vue'
import CodeView from '@/components/CodeView.vue'

export default {
  components: { CodeView },
  setup() {
    const awesome = ref(true)
    return { awesome }
  }
}
</script>

<template>
  <h1>条件渲染</h1>
  <h2>v-if</h2>
  <p>v-if 指令用域条件性地渲染一块内容。</p>
  <p>这块内容只会在指令的表达式返回真时才被渲染。</p>
  <CodeView content="<h1 v-if='awesome'>Vue is awesome!</h1>" />
  <h1 v-if="awesome">Vue is awesome!</h1>
</template>

<style></style>
