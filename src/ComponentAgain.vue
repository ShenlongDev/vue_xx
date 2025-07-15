<script setup>
import { ref } from 'vue'
import PostBlog from './components/PostBlog.vue';

const postsArray = ref([
  { title: 'Hello World' },
  { title: 'Hello Vue' },
  { title: 'Hello Vue 3' }
])
</script>


<template>
  <h1>组件基础</h1>
  <h2>传递 Props</h2>
  <p>
    如果我们正在构建一个博客，我们可能需要一个博客文章的组件。
    我们希望所有的博客文章分享相同的视觉布局，但不同的内容。
    要实现这样的效果自然必须想组件中传递数据，例如每篇文章标题和内容，这就会使用到 Props。
  </p>
  <p>
    Props 是一种特别的 attributes，你可以在组件上声明注册。
    要传递给博客文章组件一个标题，我们必须在组件的 props 列表上声明它。
    这里要用到 defineProps 宏：
  </p>
  <p>
    defineProps 是一个仅 script setup 中可用的编译宏命令，并不需要显式地导入。
    声明的 Props 会自动暴露给模板。
    defineProps 会返回一个对象，其中包含了可以传递给组件的所有 props：
  </p>
  <p>
    TypeScript 用户请参考：为组件 props 标注类型
  </p>
  <p>
    如果你没有使用 script setup，props 必须以 props 选项的方式声明，props 对象会作为 setup() 函数的第一个参数被传入。
    <pre>
      <code>
        export default {
          props: ['title'],
          setup(props) {
            console.log(props.title)
          }
        }
      </code>
    </pre>
    一个组件可以有任意多的 props，默认情况下，所有 prop 都接受任意类型的值。
  </p>
  <p>
    当一个 prop 被注册后，可以想这样以自定义 attribute 的形式传递数据给它：
  </p>
  <PostBlog title="Hello Wrold" />
  <PostBlog title="Hello Vue" />
  <post-blog title="Hello Vue 3" />
  <p>
    在实际应用中，我们可能在父组件中会有如下的一个博客文章数组：
    这种情况下，我们可以使用 v-for 来渲染他们：
  </p>
  <PostBlog v-for="post in postsArray" :key="post.title" :title="post.title" />
  <p>
    留意我们是如何使用 v-bind 语法 (:title="post.title") 来传递动态 prop 值的。当事先不知道要渲染的确切内容时，这一点特别有用。
    以上就是目前你需要了解的关于 props 的全部了。如果你看完本章节后还想知道更多细节，我们推荐你深入阅读关于 props 的完整指引。
  </p>
</template>
