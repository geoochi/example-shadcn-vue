<script setup lang="ts">
import {
  TagsInput,
  TagsInputInput,
  TagsInputItem,
  TagsInputItemDelete,
  TagsInputItemText,
} from '@/components/ui/tags-input'
import { ref } from 'vue'

const modelValue = ref(['Apple', 'Banana'])
</script>

<template>
  <div class="flex flex-col items-center gap-4">
    <TagsInput v-model="modelValue">
      <TagsInputItem v-for="item in modelValue" :key="item" :value="item">
        <TagsInputItemText />
        <TagsInputItemDelete />
      </TagsInputItem>

      <TagsInputInput placeholder="Fruits..." />
    </TagsInput>
    <p>current value: {{ modelValue }}</p>
  </div>
</template>
