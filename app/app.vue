<script setup lang="ts">
useHead({
  titleTemplate: (titleCunk) => {
    return titleCunk ? `${titleCunk} - Our Pomodoro App` : "Our Pomodoro App";
  },

	link: [
	{ rel: 'icon', type: 'image/x-icon', href: `/clock60.svg`}
	]
});
</script>

<template class="min-h-full">
  <NuxtLayout>
    <NuxtPage />
  </NuxtLayout>
</template>


