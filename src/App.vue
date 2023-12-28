<script setup lang="ts">
import { computed, reactive, ref } from 'vue';
import MfmFrames from './components/MfmFrames.vue';

const content = reactive([""]);
const output = computed(() => generate(height.value, width.value, content, 1 / fps.value));
const height = ref(0);
const width = ref(99999);
const fps = ref(1);

function generate(h: number, w: number, arr: string[], speed = 1) {
  const fn = (arr: string[], i: number): string => {
    return `$[spin.speed=${((arr.length - 1) * speed).toFixed(5)}s,delay=${(i * speed).toFixed(5)}s $[spin.speed=${((arr.length - 1) * speed).toFixed(5)}s,delay=${(i * speed).toFixed(5)}s,alternate $[position.x=${w} ${arr[i]}]]]${i + 1 < arr.length ? `\n$[position.y=-${h} ${fn(arr, i + 1)}]` : ""}`;
  }

  return `$[position.x=-${w} ${fn(arr, 0)}]`;
}
</script>

<template>
  <div class="flex flex-col w-full h-full overflow-x-hidden">
    <h1>MFMでコマ送りするやつ</h1>
    <div class="flex flex-row gap-2 w-full h-full p-2 overflow-hidden">
      <div class="flex flex-col gap-2 w-full h-full">
        <div class="grid gap-2" style="grid-template-columns: 0fr 1fr;">
          <span class="w-max flex items-center">縦幅</span>
          <input class="w-full" type="number" v-model="height" />
          <span class="w-max flex items-center">横幅</span>
          <input class="w-full" type="number" v-model="width" />
          <span class="w-max flex items-center">FPS</span>
          <input class="w-full" type="number" v-model="fps" />
        </div>
        <MfmFrames :content="content"></MfmFrames>
      </div>
      <div class="flex flex-col gap-2 w-full h-full">
        <p>出力結果</p>
        <textarea class="w-full h-full" v-model="output"></textarea>
      </div>
    </div>
  </div>
</template>
