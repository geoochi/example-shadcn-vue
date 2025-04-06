<script setup lang="ts">
import { Alert, AlertDescription, AlertTitle } from '@/components/ui/alert'
import { AlertCircle, Rocket } from 'lucide-vue-next'
</script>

<template>
  <div class="flex flex-col gap-4 w-full max-w-md">
    <Alert>
      <Rocket class="w-4 h-4" />
      <AlertTitle>Heads up!</AlertTitle>
      <AlertDescription> You can add components to your app using the cli. </AlertDescription>
    </Alert>
    <Alert variant="destructive">
      <AlertCircle class="w-4 h-4" />
      <AlertTitle>Error</AlertTitle>
      <AlertDescription> Your session has expired. Please log in again. </AlertDescription>
    </Alert>
  </div>
</template>
