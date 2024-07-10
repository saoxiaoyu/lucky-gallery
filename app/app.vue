<script setup lang="ts">
const { getImages } = useFile()

useHead({
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'en'
  }
})

const title = 'Lucky-Gallery'
const description = 'Event Photo Waterfall.'

useSeoMeta({
  title,
  ogTitle: title,
  description,
  ogDescription: description,
  ogSiteName: 'Lucky-Gallery',
  ogImage: 'https://saoxiaoyu.github.io/picx-images-hosting/17_Sheep.5kwzh7b9uzk0.png',
  twitterCard: 'summary_large_image'
})

await getImages()
</script>

<template>
  <div
    class="bg-black min-h-[100dvh] overflow-x-auto relative"
    :class="{ 'flex flex-col md:block': $router.currentRoute.value.fullPath !== '/' }"
  >
    <UNotifications />
    <NuxtPage />
    <ImageThumbnailList :class="$router.currentRoute.value.fullPath !== '/' ? 'opacity-100 z-[9999]' : 'opacity-0 z-[-1]'" />
  </div>
</template>
