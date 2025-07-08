<script setup>
import { ref, watch, reactive, watchEffect } from 'vue'

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

watchEffect(async () => {
  const response = await fetch(
    `https://jsonplaceholder.typicode.com/todos/${todoId.value}`
  )
  data.value = await response.json()
})

watch(id, (newId) => {
  fetch(`/api/${newId}`).then(() => {
    // 回调逻辑
  })
})
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
  特别是注意侦听器时如何两次使用 todoId 的，一次时作为源，另一次时在回调中。
  我们可以用 watchEffect 函数来嘉华上面的代码。
  watchEffect（）允许我们自动跟中回调的响应式依赖。
  上面的侦听器可以重写为：
  这个例子中，回调会立即执行，不需要指定 immediate: true。在执行期间，它会自动追踪 todoId.value 作为依赖（和计算属性类似）。每当 todoId.value 变化时，回调会再次执行。有了
  watchEffect()，我们不再需要明确传递 todoId 作为源值。

  你可以参考一下这个例子的 watchEffect 和响应式的数据请求的操作。

  对于这种只有一个依赖项的例子来说，watchEffect() 的好处相对较小。但是对于有多个依赖项的侦听器来说，使用 watchEffect()
  可以消除手动维护依赖列表的负担。此外，如果你需要侦听一个嵌套数据结构中的几个属性，watchEffect() 可能会比深度侦听器更有效，因为它将只跟踪回调中被使用到的属性，而不是递归地跟踪所有的属性。

  watch vs. watchEffect​
  watch 和 watchEffect 都能响应式地执行有副作用的回调。它们之间的主要区别是追踪响应式依赖的方式：

  watch 只追踪明确侦听的数据源。它不会追踪任何在回调中访问到的东西。另外，仅在数据源确实改变时才会触发回调。watch 会避免在发生副作用时追踪依赖，因此，我们能更加精确地控制回调函数的触发时机。

  watchEffect，则会在副作用发生期间追踪依赖。它会在同步执行过程中，自动追踪所有能访问到的响应式属性。这更方便，而且代码往往更简洁，但有时其响应性依赖关系会不那么明确。

  副作用清理
  又是我们可能会在侦听器中执行副作用，例如异步请求：
  watch(id, (newId) => {
  fetch(`/api/${newId}`).then(() => {
  // 回调逻辑
  })
  })

  但是如果在请求完成之前 id 发生了变化怎么办？当上一个请求完成时，它仍会使用已经过时的 ID 值触发回调。理想情况下，我们希望能够在 id 变为新值时取消过时的请求。
  我们可以使用 onWatcherCleanup() API 来注册一个清理函数，当侦听器失效并准备重新运行时会被调用：
  import { watch, onWatcherCleanup } from 'vue'

  watch(id, (newId) => {
  const controller = new AbortController()

  fetch(`/api/${newId}`, { signal: controller.signal }).then(() => {
  // 回调逻辑
  })

  onWatcherCleanup(() => {
  // 终止过期请求
  controller.abort()
  })
  })

  请注意，onWatcherCleanup 仅在 Vue 3.5+ 中支持，并且必须在 watchEffect 效果函数或 watch 回调函数的同步执行期间调用：你不能在异步函数的 await 语句之后调用它。

  作为替代，onCleanup 函数还作为第三个参数传递给侦听器回调，以及 watchEffect 作用函数的第一个参数：

  watch(id, (newId, oldId, onCleanup) => {
  // ...
  onCleanup(() => {
  // 清理逻辑
  })
  })

  watchEffect((onCleanup) => {
  // ...
  onCleanup(() => {
  // 清理逻辑
  })
  })
  这在 3.5 之前的版本有效。此外，通过函数参数传递的 onCleanup 与侦听器实例相绑定，因此不受 onWatcherCleanup 的同步限制。

  回调的触发时机

  当你更改了响应式状态，它可能会同时触发 Vue 组件更新和侦听器回调。

  类似于组件更新，用户创建的侦听器回调函数也会被批量处理以避免重复调用。例如，如果我们同步将一千个项目推入被侦听的数组中，我们可能不希望侦听器触发一千次。

  默认情况下，侦听器回调会在父组件更新 (如有) 之后、所属组件的 DOM 更新之前被调用。这意味着如果你尝试在侦听器回调中访问所属组件的 DOM，那么 DOM 将处于更新前的状态。

  如果想在侦听器回调中能访问被 Vue 更新之后的所属组件的 DOM，你需要指明 flush: 'post' 选项：

  js
  watch(source, callback, {
  flush: 'post'
  })

  watchEffect(callback, {
  flush: 'post'
  })

  后置刷新的 watchEffect() 有个更方便的别名 watchPostEffect()：

  js
  import { watchPostEffect } from 'vue'

  watchPostEffect(() => {
  /* 在 Vue 更新后执行 */
  })
</template>
