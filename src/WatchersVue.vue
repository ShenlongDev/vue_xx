<script setup>
import { ref, watch } from 'vue'

const question = ref('')
const answer = ref('Questions usually contain a question mark. ;-)')
const loading = ref(false)

// 可以直接侦听一个 ref
watch(question, async (newQuestion, oldQuestion) => {
  if (newQuestion.includes('?')) {
    loading.value = true
    answer.value = 'Thinking...'
    try {
      const res = await fetch('https://yesno.wtf/api')
      answer.value = (await res.json()).answer
    } catch (error) {
      answer.value = 'Error! Could not reach the API. ' + error
    } finally {
      loading.value = false
    }
  }
})

const x = ref(0)
const y = ref(0)

// 单个 ref
watch(x, (newX) => {
  console.log(`x is ${newX}`)
})

// getter 函数
watch(
  () => x.value + y.value,
  (sum) => {
    console.log(`sum of x + y is: ${sum}`)
  }
)

// 多个来源组成的数组
watch(
  [x, () => y.value],
  ([newX, newY]) => {
    console.log(`x is ${newX} and y is ${newY}`)
  }
)
</script>

<template>
  <h1>侦听器</h1>
  <h2>基本实例</h2>
  <p>计算属性允许我们生命性地计算衍生值。然而在有些情况下，我们需要在状态变化时执行一些“副作用”：例如更改 DOM，或是根据异步操作的结果去修改另一处的状态。</p>
  <p>地计算衍生值。然而在有些情况下，我们需要在状态变化时执行一些“副作用”：例如更改 DOM，或是根据异步操作的结果去修改另一处的状态。</p>
  <p>
    Ask a yes/no question:
    <input v-model="question" :disabled="loading" />
  </p>
  <p>{{ answer }}</p>

  <h3>侦听数据源类型</h3>
  <p>watch 的第一个参数可以是不同形式的“数据源”：它可以是一个 ref（包括计算属性），一个响应式对象，一个 getter 函数，或多个数据组成的数据：</p>
  <p>注意，你不能直接侦听响应式对象的属性值，例如：</p>
  <pre>const obj = reactive({ count: 0 })

// 错误，因为 watch() 得到的参数是一个 number
watch(obj.count, (count) => {
  console.log(`Count is: ${count}`)
})</pre>
  <p>这里需要用一个返回该属性的 getter 函数：</p>
  <pre>// 提供一个 getter 函数
watch(
  () => obj.count,
  (count) => {
    console.log(`Count is: ${count}`)
  }
)</pre>
</template>

