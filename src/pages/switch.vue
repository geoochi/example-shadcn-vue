<script setup lang="ts">
import { Label } from '@/components/ui/label'
import { Switch } from '@/components/ui/switch'
import { useDark } from '@vueuse/core'

const isDark = useDark()
</script>

<template>
  <div class="flex items-center space-x-2">
    <Switch id="airplane-mode" v-model="isDark" />
    <Label for="airplane-mode">Dark Mode: {{ isDark }}</Label>
  </div>
</template>
