<template>
  <q-layout view="hHh lpr lFf">

    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title>Nana</q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" bordered>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="footer" >
      <q-toolbar class="q-px-md q-py-sm flex flex-center" style="width: 100%">
        <q-scroll-area class="flex flex-center" style="height: 23vh; max-width: 1000px; width: 100%;">
          <q-editor
            ref="editorRef"
            v-model="newMessage"
            placeholder="请输入消息..."
            bordered
            style="width: 90%"
            @keydown.ctrl.enter.prevent="sendMessage"
            autofocus
            :input-style="{ minHeight: '48px' }"
            autogrow
            max-height="100%"
          />

        </q-scroll-area>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

// >>>>> 确保 editorRef 被定义以便访问 q-editor API <<<<<
const editorRef = ref(null);

const leftDrawerOpen = ref(false);
// newMessage 绑定 q-editor 的 v-model (HTML 内容)
const newMessage = ref('');

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value;
};

const sendMessage = () => {
  // >>>>> 通过 editorRef 获取原始 Markdown 内容 <<<<<
  const markdownContent = editorRef.value ? editorRef.value.getMarkdown() : newMessage.value;

  // 基本检查内容是否为空
  const plainText = markdownContent.replace(/<[^>]*>/g, '').trim();

  if (!plainText) {
    return;
  }
  console.log("待发送消息 (Markdown):", markdownContent);

  // TODO: 处理和发送 markdownContent

  // 清空编辑器 (清空 v-model，编辑器内容也会清空)
  newMessage.value = '';
};


</script>

<style lang="scss" scoped>
.footer{
  background: transparent;
  display: flex;
  align-items: center; /* 使 toolbar 在 footer 中垂直居中 */}

</style>
