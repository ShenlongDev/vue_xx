<script setup>
import { ref, watch, reactive } from 'vue'

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

const obj = reactive({ count: 0 })

watch(obj, (newValue, oldValue) => {
  // 在嵌套的属性变更时触发
  // 注意：`newValue` 此处和 `oldValue` 是相等的
  // 因为它们是同一个对象！
  console.log(newValue)
  console.log(oldValue)
})

obj.count++

watch(
  () => obj.count,
  (newValue, oldValue) => {
    // 注意：`newValue` 此处和 `oldValue` 是相等的
    // *除非* state.someObject 被整个替换了
  },
  { deep: true }
)

watch(
  source,
  (newValue, oldValue) => {
    // 立即执行，且当 `source` 改变时再次执行
  },
  { immediate: true }
)

watch(
  source,
  (newValue, oldValue) => {
    // 当 `source` 变化时，仅触发一次
  },
  { once: true }
)

const todoId = ref(1)
const data = ref(null)

watch(
  todoId,
  async () => {
    const response = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
    )
    data.value = await response.json()
  },
  { immediate: true }
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

  <h2>深层侦听器</h2>
  <p>直接给 watch() 传入一个响应式对象，会隐式地创建一个深层侦听器——该回调函数在所有嵌套的变更时都会被触发：</p>
  <p>相比之下，一个返回响应式对象的 getter 函数，只有在返回不同的对象是，才会触发回调：</p>
  <p>你也可以给上面这个例子显式地加上 deep 选项，强制转成深层侦听器：</p>
  <p>在 Vue 3.5+ 中，deep 选项还可以是一个数字，表示最大遍历深度——即 Vue 应该遍历对象嵌套属性的级数。</p>

  <h2>即时回调的侦听器</h2>
  <p>watch 默认是懒执行的：仅当数据源变化时，才会执行回调。但在某些场景中，我们希望在创建侦听器时，立即执行一遍回调。举例来说，我们想请求一些初始数据，然后在相关状态更改时重新请求数据。</p>
  <p>我们可以通过传入 immediate：true 选项来强制侦听器的回调立即举行：</p>

  <h2>一次性侦听器</h2>
  <p>仅支持 3.4 及以上版本</p>
  <p>每当被侦听员发生辩护时，侦听器的回调就会执行。如果希望回调只在原变化是触发一次，使用 once：true 选项。</p>

  <h2>watchEffect()</h2>
  <p>侦听器的回调使用与源完全相同的响应式状态时很常见的。例如下面的代码，在每当 todoId 的引用发生变化时使用侦听器来加载一个远程资源：</p>
</template>
