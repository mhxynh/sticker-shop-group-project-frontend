<script setup lang="ts">
import CoreNavbar from '@/components/CoreNavbar.vue'
import StickerGridItem from '@/components/StickerGridItem.vue'
</script>

<template>
  <main>
    <CoreNavbar />
    <div class="container">
      <div class="row row-cols-auto gy-4">
        <li v-for="i in 10" :key="i">
          <StickerGridItem :text="`sample text ${i}`" />
        </li>
      </div>
    </div>
  </main>
</template>

<style scoped>
</style>
