<template>
  <h2>Prop 校验</h2>
  <p>Vue 组件可以更细致地声明对传入的 props 的校验要求。比如我们上面已经看到过的类型声明，如果传入的值不满足类型要求，Vue 会在浏览器控制台中抛出警告来提醒使用者。这在开发给其他开发者使用的时候非常有用。</p>
  <p>要声明对 props 的校验，你可以向 defineProps 宏提供一个带有 props 校验选项的对象，例如：</p>
  <p>一些补充细节：</p>
  <ul>
    <li>所有 prop 默认是可选的，除非声明了 required：true。</li>
    <li>除 Boolean 外的未传递的可选 prop 将会有一个默认值 undefined。</li>
    <li>Boolean 类型的未传递的 prop 将被转换为 false。这可以通过为它设置 default 来更改——例如：设置为 default：undefined 将于非布尔类型的 prop 的行为保持一致。</li>
    <li>如果声明了 default 值，那么在 prop 的值被解析为 undefined 时，无论 prop 是未传递还是显示指明的 undefined，都会改为 default 值。</li>
  </ul>
  <p>当 prop 的校验失败后，Vue 会抛出一个控制台警告（在开发模式下）。</p>
  <!-- <p>如果使用的基于类型的 prop 声明，Vue 会尽最大努力在运行时按照 prop 的类型标注进行编译。举例来说，defineProps<{ msg: string }> 会被编译为 { msg: { type: String, required: true }}。</p> -->
</template>

<script setup>
defineProps({
  // 基础类型检查
  // （给出 `null` 和 `undefined` 值则会跳过任何类型检查）
  propA: Number,
  // 多种可能的类型
  propB: [String, Number],
  // 必传，且为 String 类型
  propC: {
    type: String,
    required: true
  },
  // 必传但可为 null 的字符串
  propD: {
    type: [String, null],
    required: true
  },
  // Number 类型的默认值
  propE: {
    type: Number,
    default: 100
  },
  // 对象类型的默认值
  propF: {
    type: Object,
    // 对象或数组的默认值
    // 必须从一个工厂函数返回。
    // 该函数接收组件所接收到的原始 prop 作为参数。
    default(rawProps) {
      console.log(rawProps)
      return { message: 'hello' }
    }
  },
  // 自定义类型校验函数
  // 在 3.4+ 中完整的 props 作为第二个参数传入
  propG: {
    validator(value, props) {
      console.log(props)
      // The value must match one of these strings
      return ['success', 'warning', 'danger'].includes(value)
    }
  },
  // 函数类型的默认值
  propH: {
    type: Function,
    // 不像对象或数组的默认，这不是一个
    // 工厂函数。这会是一个用来作为默认值的函数
    default() {
      return 'Default function'
    }
  }
})
</script>
