<script setup lang="ts">
import { ScrollArea } from '@/components/ui/scroll-area'
import { Separator } from '@/components/ui/separator'

const tags = Array.from({ length: 50 }).map((_, i, a) => `v1.2.0-beta.${a.length - i}`)
</script>

<template>
  <ScrollArea class="max-h-[300px] h-full max-w-[200px] w-full rounded-md border">
    <div class="p-4">
      <h4 class="mb-4 text-sm font-medium leading-none">Tags</h4>

      <div v-for="tag in tags" :key="tag">
        <div class="text-sm">
          {{ tag }}
        </div>
        <Separator class="my-2" />
      </div>
    </div>
  </ScrollArea>
</template>
