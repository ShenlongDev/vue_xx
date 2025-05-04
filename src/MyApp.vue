<script setup>
  const msg = 'Hello, Vue3!'
  const rawHtml = '<span style="color: red">This should be red.</span>'
  const dynamicId = 'firstBinding'
  const isDisabled = false
  const objectOfAttrs = {
    id: 'oid',
    class: 'oclass',
    style: 'background-color: green'
  }
</script>

<template>
  <p>{{ msg }}</p>
  <p>Using text interpolation: {{ rawHtml }}</p>
  <p>Using v-html directive: <span v-html="rawHtml"></span></p>
  # Attribute binding
  <div v-bind:id="dynamicId">
    This div is for showing attribute binding.
  </div>

  # 简写
  因为v-bind非常常用，我们提供了特定的简写语法。
  <div :id="dynamicId">
    开头为：的attribute可能和一般的HTML attribute 看起来不太一样，但它的确是合法的attribute名称字符，并且所有支持Vue的浏览器都能正确解析它。此外，他们不会出现在最终渲染的DOM中。简写语法是可选的，但相信在你了解它更多的用处后，你应该会更喜欢它。
  </div>

  # 同名简写
  如果attribute的名称与绑定的JavaScript之的名称相同，那么可以进一步简化语法，省略attribute值：
  这与在JavaScript中声明对象时使用的属性简写语法类似。

  # 布尔型attribute
  布尔型attribute依据true/false值来决定attribute是否应该存在于该元素上。disabled就是最常见的例子之一。
  v-bind在这首那个场景下的行为略有不同：

  <button :disabled="isDisabled">布尔型绑定按钮</button>

  # 动态绑定多个值
  如果你有像这样的一个包含多个attribute的JavaScript对象；
  通过不带参数的v-bind，你可以将他们绑定到单个元素上。
  <div v-bind="objectOfAttrs">
    通过不带参数的v-bind，你可以将他们绑定到单个元素上。
  </div>
</template>

<style scoped>
  p {
    color: blue;
    font-size: 20px;
  }

  div#firstBinding {
    color: red;
    font-size: 24px;
  }

  #oid {
    color: yellow;
    font-size: 20px;
  }

  .oclass {
    border: 2px solid black;
  }
</style>
