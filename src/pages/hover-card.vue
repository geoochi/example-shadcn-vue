<script setup lang="ts">
import { Avatar, AvatarFallback, AvatarImage } from '@/components/ui/avatar'

import { Button } from '@/components/ui/button'
import { HoverCard, HoverCardContent, HoverCardTrigger } from '@/components/ui/hover-card'
import { CalendarIcon } from 'lucide-vue-next'
</script>

<template>
  <HoverCard>
    <HoverCardTrigger as-child>
      <Button variant="link"> @vuejs </Button>
    </HoverCardTrigger>
    <HoverCardContent class="w-80">
      <div class="flex justify-between space-x-4">
        <Avatar>
          <AvatarImage src="https://github.com/vuejs.png" />
          <AvatarFallback>VC</AvatarFallback>
        </Avatar>
        <div class="space-y-1">
          <h4 class="text-sm font-semibold">@vuejs</h4>
          <p class="text-sm">Progressive JavaScript framework for building modern web interfaces.</p>
          <div class="flex items-center pt-2">
            <CalendarIcon class="mr-2 h-4 w-4 opacity-70" />
            <span class="text-xs text-muted-foreground"> Joined January 2014 </span>
          </div>
        </div>
      </div>
    </HoverCardContent>
  </HoverCard>
</template>
