<script setup>
import { ref } from 'vue'
import PostBlog from './components/PostBlog.vue';

const postsArray = ref([
  { title: 'Hello World' },
  { title: 'Hello Vue' },
  { title: 'Hello Vue 3' }
])

const postFontSize = ref(1)
</script>


<template>
  <h1>组件基础</h1>
  <h2>监听事件</h2>
  <p>
    让我们继续关注我们的 postblog 组件。
    我们会发现有时候它需要与父组件进行交互。
    例如，要在此处实现无障碍访问的需求，将博客文章的文字能够放大，而页面的其余部分仍使用默认字号。
    在父组件中，我们可以添加一个 postFontSize ref 来实现这个效果：
    在模板中用它来控制所有博客文章的字体大小：
  </p>

  <div :style="{ fontSize: postFontSize + 'em' }">
    <PostBlog
      v-for="post in postsArray"
      :key="post.id"
      :title="post.title"
      @enlarge-text="postFontSize += 0.1"
    />
  </div>
</template>
