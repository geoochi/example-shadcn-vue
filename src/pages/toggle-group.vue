<script setup lang="ts">
import { ToggleGroup, ToggleGroupItem } from '@/components/ui/toggle-group'
import { Bold, Italic, Underline } from 'lucide-vue-next'
import { ref } from 'vue'

const modelValue = ref('bold')
</script>

<template>
  <div class="flex flex-col items-center gap-4">
    <ToggleGroup type="multiple" v-model="modelValue">
      <ToggleGroupItem value="bold" aria-label="Toggle bold">
        <Bold class="h-4 w-4" />
      </ToggleGroupItem>
      <ToggleGroupItem value="italic" aria-label="Toggle italic">
        <Italic class="h-4 w-4" />
      </ToggleGroupItem>
      <ToggleGroupItem value="underline" aria-label="Toggle underline">
        <Underline class="h-4 w-4" />
      </ToggleGroupItem>
    </ToggleGroup>
    <p>current value: {{ modelValue }}</p>
  </div>
</template>
