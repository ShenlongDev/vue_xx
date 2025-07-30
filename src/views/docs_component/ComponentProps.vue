<template>
  <h1>Props</h1>
  <h2>单向数据流</h2>
  <p>所有的 props 都遵循着单向绑定原则，props 因父组件的更新而变化，自然地将新的状态向下流往子组件，而不会逆向传递。这避免了子组件意外修改父组件的状态的情况，不然应用的数据流将很容易得混乱而难以理解。</p>
  <p>另外，每次父组件更新后，所有的子组件中的 props 都会被更新到最新值，这意味着你不应该在子组件中去更改一个 prop。若你这么做了，Vue 会在控制台向你抛出警告：</p>
</template>

<script setup>
const props = defineProps(['foo'])

// ❌ 警告！prop 是只读的！
props.foo = 'bar'
</script>
