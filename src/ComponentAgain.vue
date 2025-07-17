<template>
  <h1>组件基础</h1>
  <h2>DOM 内模板解析注意事项</h2>
  <p>如果你想在 DOM 中直接书写 Vue 模板，Vue 则必须从 DOM 中获取模板字符串。</p>
  <p>由于浏览器的原生 HTML 解析行为限制，有一些需要注意的事项。</p>

  <h3>大小写区分</h3>
  <p>
    HTML 标签和属性名称是部分大小写的，所以浏览器会把任何大写的字符串解析为小写的。
    这意味着当你使用 DOM 内的模板时，无论是 PascalCase 形式的组件名称，camelCase 形式的 prop 名称
    还是 v-on 的事件名称，都需要转换为相应等价的 kebab-case （短横线链字符）形式：
  </p>
  <!-- HTML 中的 kebab-case -->
  <blog-post post-title="hello!" @update-post="onUpdatePost"></blog-post>

  <h3>闭合标签</h3>
  <p>我们在上面的例子中已经使用过了闭合标签（self-closing tag）:</p>
  <BlogPost />
  <p>
    这是因为 Vue 的模板解析器支持任意标签使用 /> 作为标签关闭的标志。
    然而在 DOM 内模板中，我们必须显示地写出关闭标签：
  </p>
  <blog-post></blog-post>
  <p>
    这是由于 HTML 只允许一小部分特殊的元素省略其关闭标签，最常见的就是 input 和 img。
    对于其他的元素来说，如果你省略了关闭标签，原生的 HTML 解析器会认为开启的标签永远没有结束，
    用下面这个代码片段举例来说：
  </p>
  <blog-post />
  <span>Hello Vue 3</span>
  <p>将被解析为：</p>
  <blog-post>
    <span>Hello Vue 3</span>
  </blog-post>

  <h3>元素位置限制</h3>
  <p>
    某些 HTML 元素对于放在其中的元素类型有限制，例如 ul，ol，table 和 select，
    相应的，某些元素进在放置于特定的元素才会显示，例如 li，tr 和 option。
    这将导致在使用带有此类限制元素的组件时出现问题。例如：
  </p>
  <table>
    <blog-post-row></blog-post-row>
  </table>
  <p>
    自定义的组件 blog-post-row 将作为无效的内容被忽略，因而在最终呈现的输出中造成错误。
    我们可以使用特殊的 is attribute 作为一种解决方案：
  </p>
  <table>
    <tr is="vue:blog-post-row"></tr>
  </table>
</template>

<script setup>
// JavaScript 中的 camelCase
const BlogPost = {
  props: ['postTitle'],
  emits: ['updatePost'],
  template: `
    <h3>{{ postTitle }}</h3>
  `
}
</script>
