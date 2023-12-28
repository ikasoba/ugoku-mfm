<script setup lang="ts">
import MfmFrame from './MfmFrame.vue';

defineProps<{
  content: string[];
}>()
</script>

<template>
  <div class="w-full h-full flex flex-col gap-2 overflow-x-hidden overflow-y-scroll pr-2">
    <MfmFrame
      v-for="_, index in content" :title="`Frame ${index}`"
      v-model:text="content[index]"
      :removeDisabled="index == 0"
      @append-after="content.splice(index + 1, 0, '')"
      @remove="content.splice(index, 1)"
    ></MfmFrame>
  </div>
</template>