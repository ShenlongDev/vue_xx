<script setup>
import { createApp } from 'vue'

const app = createApp({})

app.component(
  // 组件的名字
  'ComponentRegister',
  // 组件的实现
  {
  template: `
    <p>这是全局注册实例</p>
  `
})
</script>
