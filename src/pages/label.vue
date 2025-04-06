<script setup lang="ts">
import { Checkbox } from '@/components/ui/checkbox'
import { Label } from '@/components/ui/label'
import { ref } from 'vue'

const accepted = ref(false)
</script>

<template>
  <div class="flex flex-col items-center gap-2">
    <div class="flex items-center gap-2">
      <Checkbox id="terms" v-model="accepted" />
      <Label for="terms">Accept terms and conditions</Label>
    </div>
    <p>{{ accepted === true ? 'accepted' : 'not accepted' }}</p>
  </div>
</template>
