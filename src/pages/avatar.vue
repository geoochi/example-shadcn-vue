<script setup lang="ts">
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'
const srcs = ['https://github.com/geoochi.png', 'https://github.com/unovue.png']
</script>

<template>
  <Avatar v-for="(src, index) in srcs" :key="src" :class="`${index !== 0 ? '-ml-4' : ''} z-${10 - index}`">
    <AvatarImage :src="src" alt="Avatar" />
    <AvatarFallback>CN</AvatarFallback>
  </Avatar>
</template>
