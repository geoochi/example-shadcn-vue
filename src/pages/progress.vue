<script setup lang="ts">
import { Progress } from '@/components/ui/progress'
import { ref, watchEffect } from 'vue'

const progress = ref(13)

watchEffect(cleanupFn => {
  const timer = setTimeout(() => (progress.value = 66), 500)
  cleanupFn(() => clearTimeout(timer))
})
</script>

<template>
  <Progress v-model="progress" class="max-w-md" />
</template>
