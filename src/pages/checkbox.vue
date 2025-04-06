<script setup lang="ts">
import { Checkbox } from '@/components/ui/checkbox'
import { ref } from 'vue'
const checked = ref(false)
</script>

<template>
  <div class="flex flex-col items-center gap-2">
    <Checkbox id="terms" v-model="checked" />
    <p>{{ checked === true ? 'checked' : 'unchecked' }}</p>
  </div>
</template>
