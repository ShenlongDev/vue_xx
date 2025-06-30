<script setup>
import { ref } from 'vue'

const cnt = ref(0)
const name = ref('Vue')

function greeting(event) {
  alert(`Hello, ${name.value}!`)

  if (event) {
    alert(event.target.tagName)
  }
}

function say(message) {
  alert(message)
}

function warn(message, event) {
  // 这里可以访问原生事件
  if (event) {
    event.preventDefault()
  }
  alert(message)
}
</script>

<template>
  <h1>事件处理</h1>

  <h2>监听事件</h2>
  <p>
    我们可以使用 v-on 指令 (简写为 @) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。
    用法：v-on:click="handler" 或 @click="handler"。
    事件处理器 (handler) 的值可以是：
    <b>1.内联事件处理器</b>：事件被触发时执行的内联 JavaScript 语句 (与 onclick 类似)。
    <b>2.方法事件处理器</b>：一个指向组件上定义的方法的属性名或是路径。
  </p>

  <h2>内联事件处理器</h2>
  <button @click="cnt++">Add 1</button>
  <p>The button above has been clicked {{ cnt }} times.</p>

  <h2>方法事件处理器</h2>
  <p>随着事件处理器的逻辑变得愈发复杂，内联代码方式变得不够灵活。</p>
  <p>因此 v-on 也可以接受一个方法名或对某个方法调用。</p>
  <button @click="greeting">Greet</button>
  <p>方法事件处理器会自动接收原生 DOM 事件并触发执行。</p>
  <p>在上面的例子中，我们能够通过被触发事件的 event.target 访问到该 DOM 元素。</p>
  <p>你也可以看看为事件处理器标注类型这一章了解更多。</p>
  <h3>方法与内联事件判断</h3>
  <p>模板编译器会通过检查 v-on 的值是否是合法的 JavaScript 标识符或属性访问路径来断定是何种形式的事件处理器。</p>
  <p>举例来说，foo、foo.bar 和 foo['bar'] 会被视为方法事件处理器，而 foo() 和 count++ 会被视为内联事件处理器。</p>

  <h2>在内联处理器中调用方法</h2>
  <p>除了直接绑定方法名，你还可以在内联事件处理器中调用方法。</p>
  <p>这允许我们向方法传入自定义参数以代替原生事件：</p>
  <button @click="say('hello')">Say hello</button>
  <button @click="say('bye')">Say bye</button>

  <h2>在内联事件处理器中访问事件参数</h2>
  <p>有时我们需要在内联事件处理器中访问原生 DOM 事件。</p>
  <p>你可以向该处理器方法传入一个特殊的 $event 变量，或者使用内联箭头函数。</p>
  <!-- 使用特殊的 $event 变量 -->
  <button @click="warn('Form cannot be submitted yet.', $event)">
    Submit
  </button>
  <!-- 使用内联箭头函数 -->
  <button @click="(event) => warn('Form cannot be submitted yet.', event)">
    Submit
  </button>

  <h2>事件修饰符</h2>
  <p>在处理事件时调用 event.preventDefault() 或 event.stopPropagation() 是很常见的。</p>
  <p>尽管我们可以直接在方法内调用，但如果方法能更专注于数据逻辑而不用去处理 DOM 事件的细节会更好。</p>
  <p>为解决这一问题，Vue为 v-on 提供了事件修饰符。</p>
  <p>修饰符是用 . 表示的指令后缀，包含以下这些：</p>
  <p>stop prevent self capture once passive</p>
  <!-- 单击事件将停止传递 -->
  <a @click.stop="doThis"></a>
  <!-- 提交事件将不再重新加载页面 -->
  <form @submit.prevent="onSubmit"></form>
  <!-- 修饰语可以使用链式书写 -->
  <a @click.stop.prevent="doThat"></a>
  <!-- 也可以只有修饰符 -->
  <form @submit.prevent></form>
  <!-- 仅当 event.target 是元素本身时才会触发事件处理器 -->
  <!-- 例如：事件处理器不来自子元素 -->
  <div @click.self="doThat">...</div>

  <h2>按键修饰符</h2>
  <p>在监听键盘事件时，我们经常需要检查特定的按键。</p>
  <p>Vue 允许在 v-on 或 @ 监听按键事件时添加按键修饰符</p>
  <!-- 仅在 `key` 为 `Enter` 时调用 `submit` -->
  <input @keyup.enter="submit" />
  <p>你可以直接使用 KeyboardEvent.key 暴露的按键名称作为修饰符，但需要转为 kebab-case 形式。</p>
  <input @keyup.page-down="onPageDown" />
  <p>在上面的例子中，仅会在 $event.key 为 'PageDown' 时调用事件处理。</p>
  <h3>按键别名</h3>
  <p>Vue 为一些常用的按键提供了别名：</p>
  <h3>系统按键修饰符</h3>
  <p>你可以使用以下系统按键修饰符来触发鼠标或键盘事件监听器，只有当按键被按下时才会触发。</p>
  <!-- Alt + Enter -->
  <input @keyup.alt.enter="clear" />
  <!-- Ctrl + 点击 -->
  <div @click.ctrl="doSomething">Do something</div>
  <!-- 当按下 Ctrl 时，即使同时按下 Alt 或 Shift 也会触发 -->
  <button @click.ctrl="onClick">A</button>
  <!-- 仅当按下 Ctrl 且未按任何其他键时才会触发 -->
  <button @click.ctrl.exact="onCtrlClick">A</button>
  <!-- 仅当没有按下任何系统按键时触发 -->
  <button @click.exact="onClick">A</button>

  <h2>鼠标按键修饰符</h2>
  <p>
    这些修饰符将处理程序限定为由特定鼠标按键触发的事件。<br>
    但请注意，.left，.right 和 .middle 这些修饰符名称是基于常见的右手用鼠标布局设定的，但实际上它们分别指代设备事件触发器的“主”、”次“，“辅助”，而非实际的物理按键。<br>
    因此，对于左手用鼠标布局而言，“主”按键在物理上可能是右边的按键，但却会触发 .left 修饰符对应的处理程序。<br>
    又或者，触控板可能通过单指点击触发 .left 处理程序，通过双指点击触发 .right 处理程序，通过三指点击触发 .middle 处理程序。<br>
    同样，产生“鼠标”事件的其他设备和事件源，也可能具有与“左”，“右”完全无关的触发模式。
  </p>
</template>
