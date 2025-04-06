<script setup lang="ts">
import { Button } from '@/components/ui/button'
import { toast } from 'vue-sonner'
</script>

<template>
  <Button variant="outline" @click="toast('Date', { description: new Date().toLocaleString() })"> Show date </Button>
</template>
