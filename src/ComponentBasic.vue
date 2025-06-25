<script setup>
import { ref } from 'vue'
import ButtonCounter from '@/components/ButtonCounter.vue'
// import BlogPost from '@/components/BlogPost.vue'
import AlertBox from '@/components/AlertBox.vue'
import Home from '@/components/tabs/HomeTab.vue'
import Posts from '@/components/tabs/PostsTab.vue'
import Archive from '@/components/tabs/ArchiveTab.vue'

const count = ref(0)

const posts = ref([
  { id: 1, title: 'My journey with Vue' },
  { id: 2, title: 'Blogging with Vue' },
  { id: 3, title: 'Why Vue is so fun' }
])

const postFontSize = ref(1)

const currentTab = ref('Home')

const tabs = {
  Home,
  Posts,
  Archive
}

// JavaScript 中的 camelCase
const BlogPost = {
  props: ['postTitle'],
  emits: ['updatePost'],
  template: `
    <h3>{{ postTitle }}</h3>
  `
}
</script>

<template>
  <h2>DOM内模板解析注意事项</h2>
  <p>如果你想在DOM中直接书写Vue模板，Vue必须从DOM中获取模板字符串。</p>
  <p>由于浏览器的原生 HTML 解析行为限制，有一些需要注意的事项。</p>
  <h3>大小写区分</h3>
  <p>HTML 标签和属性名称是部分大小写的，所以浏览器会把任何大写的字符解释为小写。</p>
  <p>这意味着当你使用 DOM 内的模板时，无论是 PascalCase 形式的组件名称，camelCase 形式的 prop 名称还是 v-on 的时间名称，都需要转换为相当等价于的 kebab-case （短横线链子）形式：</p>
  <!-- HTML 中的 kebab-case -->
  <blog-post post-title="hello!" @update-post="onUpdatePost"></blog-post>

  <h2>动态组件</h2>
  <p>有些场景会需要在两个组件间来会间切换，比如 Tab 界面：</p>
  <p>上面的列子时通过 Vue component 元素和特殊的 is attribute 实现的：</p>

  <div class="demo">
    <button
       v-for="(_, tab) in tabs"
       :key="tab"
       :class="['tab-button', { active: currentTab === tab }]"
       @click="currentTab = tab"
     >
      {{ tab }}
    </button>
	  <component :is="tabs[currentTab]" class="tab"></component>
  </div>

  <p>在上面的例子中，传给 ；is的值可以时一下几种：</p>

  <h2>通过插槽来分配内容</h2>
  <p>一些情况下我们会希望能和 HTML 元素一样向组件中传递内容</p>
  当使用 component :is="..." 来在多个组件间作切换时，被切换掉的组件会被卸载。我们可以通过 KeepAlive 组件强制被切换掉的组件仍然保持“存活”的状态。

  <AlertBox>
    Something bad happened.
  </AlertBox>

  我们期望能渲染成这样：

This is an Error for Demo Purposes

Something bad happened.

这可以通过 Vue 的自定义  元素来实现：

  如上所示，我们使用
 作为一个占位符，父组件传递进来的内容就会渲染在这里。

在演练场中尝试一下

以上就是目前你需要了解的关于插槽的所有知识了。如果你看完本章节后还想知道更多细节，请深入阅读组件插槽章节。

  <h2>监听事件</h2>
  <p>让我们继续关注我们的 BlogPost 组件。</p>
  <p>我会发现有时候它需要与父组件进行交互。</p>
  <p>例如，要在此处实现无障碍访问的需求，将博客文章的文字能够放大，而页面的其余部分仍使用默认字号。</p>
  <p>在父组件中，我们可以添加一个 postFontSize ref 来实现这个效果：</p>

  <div :style="{ fontSize: postFontSize + 'em' }">
    <BlogPost
      v-for="post in posts"
      :key="post.id"
      :title="post.title"
      @enlarge-text="postFontSize += 0.1"
    />
  </div>

  <p>然后，给 BlogPost 组件添加一个按钮：</p>
  这个按钮目前还没有做任何事情，我们想要点击这个按钮来告诉父组件它应该放大所有博客文章的文字。要解决这个问题，组件实例提供了一个自定义事件系统。父组件可以通过 v-on 或 @ 来选择性地监听子组件上抛的事件，就像监听原生 DOM 事件那样：

  因为有了 @enlarge-text="postFontSize += 0.1" 的监听，父组件会接收这一事件，从而更新 postFontSize 的值。
  我们可以通过 defineEmits 宏来声明需要抛出的事件：
  这声明了一个组件可能触发的所有事件，还可以对事件的参数进行验证。同时，这还可以让 Vue 避免将它们作为原生事件监听器隐式地应用于子组件的根元素。

  和 defineProps 类似，defineEmits 仅可用于 script setup 之中，并且不需要导入，它返回一个等同于 $emit 方法的 emit 函数。它可以被用于在组件的 script setup 中抛出事件，因为此处无法直接访问 $emit：

  <h1>组件基础</h1>
  <p>组件允许我们将 UI 划分为独立的、可重用的部分，并且可以对每个部分进行单独的思考。</p>
  <p>在实际应用中，组件常常被组织成一个层层嵌套的树状结构：</p>
  <p>这和我们嵌套HTML元素的方式类似，Vue实现了自己的组件模型，是我们可以在每个组件内封装自定义内容与逻辑。</p>
  <p>Vue同样也能很好地配合原生 Web Component。</p>
  <p>如果你想知道 Vue 组件与原生 Web Components 之间的关系，可以阅读此章节。</p>

  <h2>定义一个组件</h2>
  <p>当使用构建步骤时，我们一般会将 Vue 组件定义在一个单独的 .vue 文件中，这被叫做单文件组件（简称 SFC）：</p>

  <button @click="count++">You clicked me {{ count }} times.</button>
  <h2>使用组件</h2>
  <p>要使用一个组件，我们需要在父组件中导入它。</p>
  <p>假设我们把计数器组件放在了一个叫做 ButtonCounter.vue 的文件中，这个组件将会默认导出的形式被暴露给外部。</p>

  <ButtonCounter />

  <p>通过 script setup，导入的组件都在模板中直接可用。</p>
  <p>当然你可以全局地注册一个组件，使得它在当前应用中的任何组件上都可以使用，而不需要额外再导入。</p>
  <p>关于组件的全局注册和局部注册两种方式的利弊，我们放在了组件注册这一章节中专门讨论。</p>
  <p>组件可以被宠用任意多次。</p>

  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />
  <ButtonCounter />

  <p>你会注意到，每当点击按钮时，每一个组件都维护者自己的状态，是不同的count。</p>
  <p>这是因为每当发你使用组件，就创建了一个新的实例。</p>
  <p>在单文件组件中，推荐使用 PascalCase的标签名，一次来和原生的HTML元素做区分。</p>
  <p>虽然原生 HTML 标签名是不区分大小写的，但 Vue 单文件组件是可以在编译中区分大小写的。</p>
  <p>我们也可以使用 /> 来关闭一个标签。</p>
  <p>如果你是直接在 DOM 中书写模板 (例如原生 template 元素的内容)，模板的编译需要遵从浏览器中 HTML 的解析行为。</p>
  <p>在这种情况下，你应该需要使用 kebab-case 形式并显式地关闭这些组件的标签。</p>

  <h2>传递Props</h2>
  <p>如果我们正在构建一个博客，我们可能需要一个表示博客文章的组件。</p>
  <p>我们希望所有的博客文章分享相同的视觉布局，担忧不同的内容。</p>
  <p>要实现真样的效果自然必须想组件中传递数据，例如每篇文章标题和内容，这就会使用到props。</p>
  <p>Props 时一种特别的 attributes，你可以在组件上声明注册。</p>
  <p>要传递个博客文章组件一个标题，我们必须在组件的 props 列表上声明它。</p>
  <p>这里要用到 defineProps 宏：</p>
  <p>defineProps 是一个仅 script setup 中可用的编译宏命令，并不需要显示地导入。</p>
  <p>生命的 props 会自动暴露给模板。</p>
  <p>defineProps 会返回一个对象，其中包含了可以传递给组件的所有 props：</p>
  <p>当一个Prop被注册的后，可以想这样自定义 attribute 的形式床底数据给它：</p>

  <BlogPost title="My journey with Vue" />
  <BlogPost title="Blogging with Vue" />
  <BlogPost title="Why Vue is so fun" />

  <p>在实际应用中，我们可以能在父组件中会有如下的一个博客文章数组：</p>

  <BlogPost
    v-for="post in posts"
    :key="post.id"
    :title="post.title"
  />

  <p>留意我们是如何使用 v-bind 语法 (:title="post.title") 来传递动态 prop 值的。当事先不知道要渲染的确切内容时，这一点特别有用。</p>
  <p>以上就是目前你需要了解的关于 props 的全部了。如果你看完本章节后还想知道更多细节，我们推荐你深入阅读关于 props 的完整指引。</p>
</template>
