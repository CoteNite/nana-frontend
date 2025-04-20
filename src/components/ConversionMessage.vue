<script setup>
import MarkdownText from 'components/MarkdownText.vue'
// ref is not used, can remove
// import { ref } from 'vue'

const props = defineProps({
  isUser:{
    type: Boolean,
    required: true,
  },
  user: {
    type: Object,
    required: true,
    validator: (value) => {
      return value !== null && typeof value === 'object' &&
        typeof value.username === 'string' && typeof value.avatar === 'string';
    }
  },
  message: {
    type: String,
    required: true,
  },
})

</script>

<template>
  <q-item class="q-px-none q-py-xs">

    <q-item-section v-if="!props.isUser" side top avatar class="q-mr-sm">
      <q-avatar rounded size="36px">
        <img :src="props.user.avatar" :alt="`${props.user.username} 的头像`" />
      </q-avatar>
    </q-item-section>

    <q-item-section :class="['message-bubble', {'user-message-bubble': props.isUser}]">
      <q-item-label class="text-bold">{{ props.user.username }}</q-item-label>
      <MarkdownText :text="props.message" class="shadow-5" />
    </q-item-section>

    <q-item-section v-if="props.isUser" side top avatar class="q-ml-sm">
      <q-avatar rounded size="36px">
        <img :src="props.user.avatar" :alt="`${props.user.username} 的头像`" />
      </q-avatar>
    </q-item-section>

  </q-item>
</template>

<style scoped lang="scss">

// 消息气泡的基础样式
.message-bubble {

  // 气泡内边距
  padding: 8px 12px;

  // 气泡圆角
  border-radius: 12px;

  // 确保文本自动换行
  word-wrap: break-word;
  overflow-wrap: break-word;
}


// 确保 q-item 的子项（头像和消息气泡节）顶部对齐
.q-item {
  align-items: flex-start; // 使 Flex 子项顶部对齐
}



</style>
