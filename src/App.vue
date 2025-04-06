<script setup lang="ts">
import { useDark, useMagicKeys } from '@vueuse/core'
import { watch } from 'vue'
import { useRouter } from 'vue-router'
import { Toaster } from '@/components/ui/sonner'

import '@/global.css'

useDark()
const router = useRouter()
const pageIgnores = ['/page-dashboard', '/page-doc', '/sidebar']
const { escape } = useMagicKeys()
watch(escape, v => {
  if (v) router.push('/')
})
</script>

<template>
  <Toaster />
  <div class="flex h-screen flex-col">
    <p
      v-if="!pageIgnores.includes(router.currentRoute.value.path)"
      class="text-center text-8xl text-gray-100 dark:text-gray-900"
    >
      press esc to go home
    </p>
    <div class="flex flex-1 items-center justify-center">
      <RouterView />
    </div>
  </div>
</template>
