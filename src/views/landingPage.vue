<script setup lang="ts">
const mobileImage = new URL('@/assets/mobile/Building.png', import.meta.url).href;
const tabletImage = new URL('@/assets/tablet/Building.png', import.meta.url).href;
const desktopImage = new URL('@/assets/desktop/Building.png', import.meta.url).href;
import { ref, onMounted, onUnmounted, markRaw } from 'vue';

import landingDesktop from '@/components/desktop/landingDesktop.vue';
import landingTablet from '@/components/tablet/landingTablet.vue';
import landingMobile from '@/components/mobile/landingMobile.vue';

const components = {
  desktop: markRaw(landingDesktop),
  tablet: markRaw(landingTablet),
  mobile: markRaw(landingMobile),
};

const currentComponent = ref(components.mobile);

function updateComponent() {
  const width = window.innerWidth;

  if (width >= 1025) {
    currentComponent.value = components.desktop;
  } else if (width >= 769) {
    currentComponent.value = components.tablet;
  } else {
    currentComponent.value = components.mobile;
  }
}

onMounted(() => {
  updateComponent();
  window.addEventListener('resize', updateComponent);
});

onUnmounted(() => {
  window.removeEventListener('resize', updateComponent);
});
</script>

<template>
  <div class="w-full h-screen flex flex-col justify-center items-center bg-[#cbdbfc]">
    <component :is="currentComponent" />
  </div>
  <div class="flex justify-center items-center bg-[#cbdbfc]">
    <picture>
      <source :srcset="mobileImage" media="(max-width: 769px)">
      <source :srcset="tabletImage" media="(max-width: 1025px)">
      <img :src="desktopImage" alt="Building" loading="lazy">
    </picture>
  </div>
</template>
