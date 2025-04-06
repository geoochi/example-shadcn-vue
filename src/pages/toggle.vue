<script setup lang="ts">
import { Toggle } from '@/components/ui/toggle'
import { Bold } from 'lucide-vue-next'
import { ref } from 'vue'

const isBold = ref(false)
</script>

<template>
  <div class="flex flex-col items-center gap-4">
    <Toggle aria-label="Toggle italic" v-model="isBold">
      <Bold class="h-4 w-4" />
    </Toggle>
    <p>isBold: {{ isBold }}</p>
  </div>
</template>
