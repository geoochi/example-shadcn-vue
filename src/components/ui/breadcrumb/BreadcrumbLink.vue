<script lang="ts" setup>
import type { HTMLAttributes } from 'vue'
import { cn } from '@/lib/utils'
import { RouterLink } from 'vue-router'

const props = defineProps<{
  class?: HTMLAttributes['class']
  to: string
}>()
</script>

<template>
  <RouterLink data-slot="breadcrumb-link" :to="to" :class="cn('hover:text-foreground transition-colors', props.class)">
    <slot />
  </RouterLink>
</template>
