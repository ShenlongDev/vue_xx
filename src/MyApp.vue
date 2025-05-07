<script setup>
import { nextTick } from 'vue'

async function increment() {
  count.value++
  await nextTick()
  // 现在 DOM 已经更新了
}
</script>

<template>
  # DOM更新时机
  当你修改了响应式状态时，DOM会被自动更新。但是要注意的是，DOM更新不是同步的。
  Vue会在’next tick‘更新周期中缓冲所有状态的修改，以确保不管你进行了多少次状态修改，每个组件都值会被更新一次。

  要等待DOM更行完成后在举行额外的代码，可以使用nextTick()全局API：
</template>

<style scoped></style>
