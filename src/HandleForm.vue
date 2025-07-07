<script setup>
import { ref } from 'vue'

const text = ref('')
const message = ref('')
const checkedNames = ref([])

const selected = ref('A')

const options = ref([
  { text: 'One', value: 'A' },
  { text: 'Two', value: 'B' },
  { text: 'Three', value: 'C' }
])

const lazymsg = ref('')
</script>

<template>
  <h1>表单输入绑定</h1>

  <p>在前端处理表单时，我们常常需要将表单输入框的内容同步给 JavaScript 中相应的变量。</p>
  <p>手动连接值绑定和更改事件监听器可能会很麻烦：</p>
  <input
    :value="text"
    @input="event => text = event.target.value">
  <p>v-model 指令帮我们简化了这一步骤：</p>
  <input v-model="text">
  <p>另外， v-model 还可以用域各种不同类型的输入，textarea，select 元素。</p>
  <p>他会根据所使用的元素自动使用对应的 DOM 属性和事件组合：</p>
  <ol>
    <li>文本类型的 input 和 textarea 元素会绑定 value property 并侦听 input 事件；</li>
    <li>checkbox 和 radio 会绑定 checked property 并侦听 change 事件；</li>
    <li>select 会绑定 value property 并侦听 change 事件。</li>
  </ol>

  <h2>基本用法</h2>
  <h3>文本</h3>
  <p>Message is: {{ message }}</p>
  <input v-model="message" placeholder="edit me" />
  <h3>多行文本</h3>
  <span>Multiline message is:</span>
  <p style="white-space: pre-line;">{{ message }}</p>
  <textarea v-model="message" placeholder="add multiple lines"></textarea>
  <p>注意在 textarea 中是不支持插值表达式的。请使用 v-model 来替代：</p>
  <!-- 错误 -->
  <textarea>{{ text }}</textarea>
  <!-- 正确 -->
  <textarea v-model="text"></textarea>
  <h3>复选框</h3>
  <p>单一的复选框，绑定布尔类型值：</p>
  <input type="checkbox" id="checkbox" v-model="checked" />
  <label for="checkbox">{{ checked }}</label>
  <p>我们也可以将多个复选框绑定到同一个数组或集合的值：</p>
  <div>Checked names: {{ checkedNames }}</div>
  <input type="checkbox" id="jack" value="Jack" v-model="checkedNames" />
  <label for="jack">Jack</label>
  <input type="checkbox" id="john" value="John" v-model="checkedNames" />
  <label for="john">John</label>
  <input type="checkbox" id="mike" value="Mike" v-model="checkedNames" />
  <label for="mike">Mike</label>
  <p>在这个例子中，checkedNames 数组将始终包含所有当前被选中的框的值。</p>
  <h3>单选按钮</h3>
  <div>Picked: {{ picked }}</div>
  <input type="radio" id="one" value="One" v-model="picked" />
  <label for="one">One</label>
  <input type="radio" id="two" value="Two" v-model="picked" />
  <label for="two">Two</label>
  <h3>选择器</h3>
  <div>Selected: {{ selected }}</div>
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <p>多选 (值绑定到一个数组)：</p>
  <div>Selected: {{ selected }}</div>
  <select v-model="selected" multiple>
    <option>A</option>
    <option>B</option>
    <option>C</option>
  </select>
  <p>选择器的选项可以使用 v-for 动态渲染</p>
  <select v-model="selected">
    <option v-for="(index, option) in options" :key="index" :value="option.value" :label="option.text">
      {{ option.text }}
    </option>
  </select>
  <div>Selected: {{ selected }}</div>

  <h2>值绑定</h2>
  <p>对于单选按钮，复选框和选择器选项，v-model 绑定的值通常是静态的字符串（或者对复选框是布尔值）：</p>
  <!-- `picked` 在被选择时是字符串 "a" -->
  <input type="radio" v-model="picked" value="a" />
  <!-- `toggle` 只会为 true 或 false -->
  <input type="checkbox" v-model="toggle" />
  <!-- `selected` 在第一项被选中时为字符串 "abc" -->
  <select v-model="selected">
    <option value="abc">ABC</option>
  </select>
  <p>但有时我们可能希望将该值绑定到当前组件实例上的动态数据。
    这可以通过使用 v-bind 来实现。
    此外，使用 v-bind 还使我们可以将选项值绑定为非字符串的数据类型。
  </p>
  <h3>复选框</h3>
  <input
  type="checkbox"
  v-model="toggle"
  true-value="yes"
  false-value="no" />
  <p>true-value 和 false-value 是 Vue 特有的 attributes，仅支持和 v-model 配套使用。这里 toggle 属性的值会在选中时被设为 'yes'，取消选择时设为 'no'。你同样可以通过 v-bind 将其绑定为其他动态值：</p>
  <input
  type="checkbox"
  v-model="toggle"
  :true-value="dynamicTrueValue"
  :false-value="dynamicFalseValue" />
  <h3>单选按钮</h3>
  <input type="radio" v-model="pick" :value="first" />
  <input type="radio" v-model="pick" :value="second" />
  <p>pick 会在第一个按钮选中时被设为 first，在第二个按钮选中时被设为 second。</p>
  <h3>选择器选项</h3>
    <select v-model="selected">
    <!-- 内联对象字面量 -->
    <option :value="{ number: 123 }">123</option>
  </select>
  <p>v-model 同样也支持非字符串类型的值绑定！在上面这个例子中，当某个选项被选中，selected 会被设为该对象字面量值 { number: 123 }。</p>

  <h2>修饰符</h2>
  <h3>.lazy</h3>
  <p>默认情况下，v-model 会在每次 input 事件后更新数据。</p>
  <p>你可以加 lazy 修饰符来改为在每次 change 事件后更新数据。</p>
  <!-- 在 "change" 事件后同步更新而不是 "input" -->
  <input v-model.lazy="lazymsg" @input="console.log(lazymsg)" @change="console.log(lazymsg)" />
  <h3>.number</h3>
  <p>如果你想让用户输入自动转换为数字，你可以在 v-model 后添加 .number 修饰符来管理输入：</p>
  <input v-model.number="age" />
  <p>如果该值无法被 parseFloat() 处理，那么将返回原始值。特别是当输入为空时 (例如用户清空输入字段之后)，会返回一个空字符串。这种行为与 DOM 属性 valueAsNumber 有所不同。number 修饰符会在输入框有 type="number" 时自动启用。</p>
  <h3>.trim</h3>
  <p>如果你想要默认自动去除用户输入内容中两端的空格，你可以在 v-model 后添加 .trim 修饰符：</p>
  <input v-model.trim="msg" />

  <h2>组件上的 v-model</h2>
  <p>HTML 的内置表单输入类型并不总能满足所有需求。</p>
  <p>幸运的是，我们可以使用 Vue 构建具有自定义行为的可复用输入组件，并且这些输入组件也支持 v-model！</p>
  <p>要了解更多关于此的内容，请在组件指引中阅读配合 v-model 使用。</p>
</template>
