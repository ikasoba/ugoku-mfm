<script setup lang="ts">
defineProps<{
  title?: string;
  text?: string;
  removeDisabled?: boolean;
}>()

const emit = defineEmits<{
  appendAfter: []
  remove: []
  "update:text": [string]
}>()
</script>

<template>
  <div class="w-full">
    <div
      class="w-full flex flex-col gap-2 p-2 border border-gray-300 border-b-0 rounded-lg rounded-b-none"
    >
      <p v-if="title">{{ title }}</p>
      <textarea :value="text" @input="emit('update:text', ($event.target as HTMLInputElement).value)"></textarea>
    </div>
    <div
      class="w-full flex gap-2 p-2 border border-gray-300 rounded-lg rounded-t-none"
    >
      <button class="btn-safe" @click="emit('appendAfter')">下に新規フレーム</button>
      <button v-if="!removeDisabled" class="btn-danger ml-auto" @click="emit('remove')">削除</button>
    </div>
  </div>
</template>