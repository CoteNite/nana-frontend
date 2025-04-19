<template>
  <q-field class="q-pa-sm">
    <template v-slot:control>
      <div class="markdown-body text-grey-4" v-html="renderedHtml"/>
    </template>
  </q-field>
</template>

<script setup>
import {ref, watch } from 'vue';
import { marked } from 'marked';
import DOMPurify from 'dompurify';

// 定义组件接收的 props
const props = defineProps({
  /**
   * 需要解析和渲染的 Markdown 字符串。
   */
  text: {
    type: String,
    required: true,
  },
});

// 使用 ref 创建一个状态变量来存储渲染后的 HTML
const renderedHtml = ref(''); // 初始化为空字符串，或者可以设置为“加载中...”

const parseAndSanitize = async (markdownText) => {

  if (!markdownText) {
    renderedHtml.value = '';
    return;
  }


    const html = await marked.parse(markdownText);

    // 使用 DOMPurify 净化 HTML，移除潜在的危险内容
    const cleanHtml = DOMPurify.sanitize(html);

    // 更新状态变量的值
    renderedHtml.value = cleanHtml;

};

watch(() => props.text, (newText) => {
  parseAndSanitize(newText);
}, { immediate: true });


</script>


<style scoped lang="scss">

.markdown-body :deep(p) {
  margin-top: 0.5em;
  margin-bottom: 0.5em;

}

.markdown-body :deep(p):first-child {
  margin-top: 0;
}
.markdown-body :deep(p):last-child {
  margin-bottom: 0;
}

.markdown-body :deep(strong) {
  font-weight: bold;
}

.markdown-body :deep(em) {
  font-style: italic;
}

.markdown-body :deep(a) {
  text-decoration: underline;
}

.markdown-body :deep(ul),
.markdown-body :deep(ol) {
  margin-top: 0.5em;
  margin-bottom: 0.5em;
  padding-left: 1.5em;
}

.markdown-body :deep(li) {
  margin-bottom: 0.25em;
}

.markdown-body :deep(a) {
  color: $info;
}

</style>
