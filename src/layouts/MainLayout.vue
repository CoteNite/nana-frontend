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

    <q-footer>
      <q-toolbar class="q-px-md q-py-sm flex flex-center" style="width: 100%">
        <q-editor
          ref="editorRef"
          v-model="newMessage"
          placeholder="请输入消息..."
          bordered
          autofocus
          autogrow
          :input-style="{ minHeight: '48px' }" max-height="150px"
          style="width: 90%"
          @keydown.ctrl.enter.prevent="sendMessage"
        />
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script setup>
import { ref } from 'vue'

const editorRef = ref(null);

const leftDrawerOpen = ref(false);
const newMessage = ref('');

const toggleLeftDrawer = () => {
  leftDrawerOpen.value = !leftDrawerOpen.value;
};

const sendMessage = () => {
  const htmlContent = editorRef.value ? editorRef.value.getHTML() : newMessage.value;
  const plainText = htmlContent.replace(/<[^>]*>/g, '').trim();

  if (!plainText) {
    return;
  }
  console.log("待发送消息 (HTML):", htmlContent);

  // TODO: 处理和发送 htmlContent

  newMessage.value = '';
  if (editorRef.value) {
    // 清空后让编辑器重新获得焦点
    editorRef.value.focus();
    // 可选：如果需要清空编辑器时强制其高度回到 min-height
    // 可以尝试 await nextTick() 或 setTimeout 后设置编辑器 v-model 或调用其 clear 方法（如果暴露）
    // 但通常清空 v-model 就会自动回缩
  }
};
</script>

<style lang="scss" scoped>


</style>
