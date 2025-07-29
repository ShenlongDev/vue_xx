<template>
  <h1>Props</h1>
  <h2>传递 prop 的细节</h2>
  <h3>Prop 名字格式</h3>
  <h3>静态 vs. 动态 Props</h3>
  <h3>传递不同的值类型</h3>
  <p>在上述的两个例子中，我们只传入了字符串值，但实际上任何类型的值都可以作为 props 的值被传递。</p>
  <h4>Number</h4>
  <h4>Boolean</h4>
  <h4>Array</h4>
  <!-- 虽然这个数组是个常量，我们还是需要使用 v-bind -->
  <!-- 因为这是一个 JavaScript 表达式而不是一个字符串 -->
  <PostBlog :comment-ids="[234, 266, 273]" />
  <!-- 根据一个变量的值动态传入 -->
  <PostBlog :comment-ids="post.commentIds" />
</template>

<script setup>
import PostBlog from '@/components/PostBlog.vue'

const post = {
  title: 'This is the first post',
  author: 'super dev',
  likes: 5003,
  commentIds: [234, 266, 273]
}
</script>
