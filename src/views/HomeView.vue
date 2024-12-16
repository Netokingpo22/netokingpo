<script setup lang="ts">
import HelloWorld from '@/components/HelloWorld.vue';
const mobileImage = new URL('@/assets/mobile/Building.png', import.meta.url).href;
const tabletImage = new URL('@/assets/tablet/Building.png', import.meta.url).href;
const desktopImage = new URL('@/assets/desktop/Building.png', import.meta.url).href;
</script>

<template>
  <div class="w-full h-screen flex justify-center items-center bg-[#cbdbfc]">
    <HelloWorld></HelloWorld>
  </div>
  <div class="flex justify-center items-center bg-[#cbdbfc]">
    <picture>
      <source :srcset="mobileImage" media="(max-width: 767px)">
      <source :srcset="tabletImage" media="(max-width: 1279px)">
      <img :src="desktopImage" alt="Building" loading="lazy">
    </picture>
  </div>
</template>
