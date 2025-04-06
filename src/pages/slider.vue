<script setup lang="ts">
import { cn } from '@/lib/utils'
import { Slider } from '@/components/ui/slider'
import { ref, watch } from 'vue'

const modelValue = ref([50])
</script>

<template>
  <div class="flex flex-col items-center gap-2">
    <Slider v-model="modelValue" :max="100" :step="1" class="w-[300px]" />
    <p>{{ modelValue[0] }}</p>
  </div>
</template>
