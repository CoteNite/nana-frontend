<script setup>
import MarkdownText from 'components/MarkdownText.vue'

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
  <q-item style="width: 45%">

    <q-item-section v-if="!props.isUser" side top avatar>
      <q-avatar rounded>
        <img :src="props.user.avatar" :alt="`${props.user.username} 的头像`" />
      </q-avatar>
    </q-item-section>

    <q-item-section>
      <q-item-label>{{ props.user.username }}</q-item-label>
      <MarkdownText :text="props.message" class=" shadow-5" />
    </q-item-section>

    <q-item-section v-if="props.isUser" side top avatar>
      <q-avatar rounded>
        <img :src="props.user.avatar" :alt="`${props.user.username} 的头像`" />
      </q-avatar>
    </q-item-section>

  </q-item>
</template>



<style scoped lang="scss">

.message{
  background: $dark;
}

</style>
