<template>
  <UContainer class="py-10">
    <div class="grid gap-8 lg:grid-cols-3">
      <!-- Left big timer -->
      <div class="lg:col-span-2">
        <WorkdayCountdown class="h-full" />
      </div>

      <!-- Right stacked timers -->
      <div class="flex flex-col gap-8">
        <PaycheckCountdown />
        <PizzaPartyCountdown />
      </div>
    </div>
  </UContainer>
</template>

<script setup lang="ts">
</script>
