<script setup>
import ConversionMessage from 'components/ConversionMessage.vue'
import { ref } from 'vue'

// 示例用户数据
const user = ref({
  username: 'CoteNite',
  avatar: '/favicon.ico',
})

// 示例消息数据
const message = ref(
  '您好！这是一条测试消息，包含一些 Markdown 格式：\n\n' +
  '这里是**加粗文本**和*斜体文本*的例子。你也可以使用 `__加粗__` 和 `_斜体_`。\n\n' +
  '这是一个列表：\n' +
  '- 列表项 1\n' +
  '- 列表项 2\n' +
  '  - 子列表项 A\n' +
  '  - 子列表项 B\n\n' +
  '这是一个有序列表：\n' +
  '1. 第一个项目\n' +
  '2. 第二个项目\n\n' +
  '这是一段引用：\n' +
  '> 这是引用块中的文字。\n' +
  '> 可以用于强调某些内容。\n\n' +
  '你可以在文本中包含 `行内代码`。\n\n' +
  '或者是一个代码块（尽管在聊天消息中不太常见）：\n' +
  '```javascript\n' +
  'const message = "Hello, Markdown!";\n' +
  'console.log(message);\n' +
  '```\n\n' +
  '这是一个链接：[访问 Quasar 官网](https://quasar.dev)\n\n' +
  '还有一个删除线文本：~~这段文字应该被删除~~\n\n' +
  '希望这段测试文本能帮助您验证 Markdown 组件的渲染效果！'
);

</script>


<template>
  <q-page class="q-px-md q-pt-md">

    <q-scroll-area style="height: 70vh;">
      <q-list class="column q-gutter-y-md">
        <ConversionMessage
          :is-user="false"
          :user="user"
          :message="message"
          class="self-start chat-message" />

        <ConversionMessage
          :is-user="true"
          :user="user"
          :message="message"
          class="self-end chat-message" />
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

<style lang="scss" scoped>
/*
  移除 q-page 的 Flex 布局设置
  移除 .q-scroll-area 中关于高度的设置，因为已使用内联样式
*/
.q-page {
  // 保留 q-px-md q-pt-md
}

.q-scroll-area {
  // 移除所有关于 height, max-height, min-height, flex-grow, flex-shrink, flex-basis 的设置
  // width 和 max-width 如果需要，可以保留在此处或移动到内联 style
  width: 100%; // 示例：确保宽度是满的
  max-width: 1000px; // 示例：如果列表本身也需要最大宽度限制
  margin: 0 auto; // 示例：如果需要列表居中
}


/*
  为消息组件设置最大宽度，防止在宽屏下拉伸过长。
  self-start 和 self-end 已经处理了左右对齐，max-width 限制宽度。
*/
.chat-message {
  max-width: 90%;

  @media (min-width: $breakpoint-sm-min) {
    max-width: 80%;
  }

  @media (min-width: $breakpoint-md-min) {
    max-width: 700px;
  }
}
</style>
