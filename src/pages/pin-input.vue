<script setup lang="ts">
import {
  PinInput,
  PinInputGroup,
  PinInputInput,
} from '@/components/ui/pin-input'
import { ref } from 'vue'

const value = ref<string[]>([])
const n = ref(6)
</script>

<template>
  <div class="flex flex-col items-center gap-2">
    <PinInput id="pin-input" v-model="value">
      <PinInputGroup>
        <PinInputInput v-for="(id, index) in n" :key="id" :index="index" />
      </PinInputGroup>
    </PinInput>
    <p>{{ value.length === n ? value.join('') : '' }}</p>
  </div>
</template>
