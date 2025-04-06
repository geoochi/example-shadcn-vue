<script setup lang="ts">
import { useRouter } from 'vue-router'
import { cn } from '@/lib/utils'

const router = useRouter()
const pages = router.getRoutes().sort((a, b) => a.path.localeCompare(b.path))
const notAvailable = ['index', '404', 'not-found']
// console.log(pages)
</script>

<template>
  <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 w-full max-w-7xl gap-4 px-4">
    <RouterLink
      v-for="route in pages.filter(route => !notAvailable.includes(route.name as string))"
      :to="route.path"
      :class="
        cn(
          'px-10 py-4 text-center outline outline-gray-300 dark:outline-gray-700',
          'rounded-md hover:bg-gray-100 dark:hover:bg-gray-900'
        )
      "
    >
      {{ route.name }}
    </RouterLink>
  </div>
</template>
