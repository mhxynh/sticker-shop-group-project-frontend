<script setup lang="ts">
import CoreNavbar from '@/components/CoreNavbar.vue'
import jotchua from '@/assets/jotchua.jpg'
import { onBeforeMount, ref } from 'vue';
import { API_URL } from '@/config';
import { useRoute } from 'vue-router';

const route = useRoute();

const stickerName = ref("");
const description = ref("");
const stickerType = ref("");
const stickerData = ref("");

onBeforeMount(async () => {
  const sticker_id = route.params.id;
  const url = `${API_URL}stickers/${sticker_id}`;

  try {
    const response = await fetch(url);

    if (response.status !== 200) return alert("Error fetching sticker data");
    
    const data = await response.json();

    stickerName.value = data.name;
    description.value = data.description;
    stickerType.value = data.sticker.type;
  } catch (error) {
    console.log(error);
  }
})
</script>

<template>
  <CoreNavbar />
  <div class="container">
    <div class="sticker-container">
      <p v-if="stickerType==='polygonal'">insert polygon here</p>
      <img v-if="stickerType==='image'" :src="jotchua" class="sticker-image" />
    </div>
    <div>
      <h2 class="mb-10">{{ stickerName }}</h2>
      <p>{{ description }}</p>
    </div>
  </div>
</template>

<style scoped lang="scss">
.container {
  display: flex;
  flex-direction: row;
}

.sticker-container {
  display: flex;
  justify-content: center;
  align-items: center;
  min-width: 50%;
  max-width: 50%;
  margin-right: 16px;
  border: 1px solid gray;
  border-radius: 8px;
  padding: 16px;
}

.sticker-image {
  width: 100%;
}
</style>
