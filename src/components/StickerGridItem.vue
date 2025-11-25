<script setup lang="ts">
import { ref } from 'vue'
import StickerImage from './StickerImage.vue';

defineProps<{
  name: string;
  stickerType: string
  imageData?: string
  shape?: string
  color?: string
}>()


const colors = ['white', 'black', 'yellow', 'cyan', 'pink', 'red', 'grey']
const selectedColor = ref('white')

function pickColor(c: string) {
  selectedColor.value = c
}
</script>

<template>
  <div class="sticker-grid-item">
    <div class="sticker-image-container" :style="{ boxShadow: `0 0 0 6px ${selectedColor}` }">
      <StickerImage
        :sticker-type="stickerType"
        :image-data="imageData"
        :shape="shape"
        color="red"
      />
    </div>
    <div class="sticker-name">
      {{ name }}
    </div>
    <div class="color-palette">
      <button
        v-for="c in colors"
        :key="c"
        class="color-swatch"
        :style="{ backgroundColor: c }"
        @click="pickColor(c)"
        :aria-label="'Pick color ' + c"
        type="button"
      ></button>
    </div>
  </div>
</template>

<style scoped>
.sticker-grid-item {
  display: flex;
  flex-direction: column;
  padding: 12px;
  border: 1px rgb(161, 157, 157) solid;
  border-radius: 12px;
  box-shadow: 2px 2px 4px rgb(116, 115, 115);
}

.sticker-image-container {
  aspect-ratio: 1/1;
  width: 100%;
  height: 100%;
  margin-bottom: 8px;
  border-radius: 10px;
  overflow: hidden;
}
.sticker-name {
  font-weight: bold;
}

.sticker-image {
  width: auto;
}

.color-palette {
  display: flex;
  gap: 8px;
  margin: 8px 0;
}
.color-swatch {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  border: 2px solid rgba(0,0,0,0.15);
  padding: 0;
  cursor: pointer;
}
</style>
