<template>
  <h1>Props</h1>
  <h2>传递 prop 的细节</h2>
  <h3>Prop 名字格式</h3>
  <h3>静态 vs. 动态 Props</h3>
  <p>至此，你已经见过了很多像这样的静态值形式的 Props：</p>
  <PostBlog title="My journey with Vue" />
  <p>相应地，还有使用 v-bind 或缩写：来进行动态绑定的 props：</p>
  <PostBlog :title="post.title + '.'" />
  <PostBlog :title="post.title + ' by ' + post.author + '.'" />
</template>

<script setup>
import PostBlog from '@/components/PostBlog.vue'

const post = {
  title: 'This is the first post',
  author: 'super dev'
}
</script>
