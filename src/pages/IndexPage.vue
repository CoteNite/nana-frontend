<script setup>
import ConversionMessage from 'components/ConversionMessage.vue'
import { ref } from 'vue'


const user = ref({
  username: 'CoteNite',
  avatar: '/favicon.ico',
})

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
  <q-page  class="q-px-md q-pt-md">

    <q-scroll-area style="height: 70vh">
      <q-list class="column q-gutter-y-md">
        <!-- 左对齐消息 -->
        <ConversionMessage
          :is-user="false"
          :user="user"
          :message="message"
          class="self-start" />

        <!-- 右对齐消息 -->
        <ConversionMessage
          :is-user="true"
          :user="user"
          :message="message"
          class="self-end" />
      </q-list>
    </q-scroll-area>
  </q-page>
</template>

