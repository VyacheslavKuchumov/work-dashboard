<template>
    <UCard 
        :ui="{
        header: 'p-0 sm:px-0', // Remove padding from header slot
        }">
        <template #header>
            <NuxtImg
            src="/images/pizza.webp"
            alt="Pizza Party Countdown"
            class="w-full h-62 object-cover rounded-t-lg"
            />
        </template>
        <p class="text-xl">Days until pizza party:</p>
        <p class="text-2xl font-semibold">{{ daysUntilPizzaParty }} days</p>
    </UCard>
</template>

<script setup lang="ts">


const daysUntilPizzaParty = computed(() => {
  const now = new Date()
  const lastDay = new Date(now.getFullYear(), now.getMonth() + 1, 0)
  let lastFriday = lastDay
  while (lastFriday.getDay() !== 5) {
    lastFriday = new Date(lastFriday.getFullYear(), lastFriday.getMonth(), lastFriday.getDate() - 1)
  }
  if (now > lastFriday) {
    const nextMonthLastDay = new Date(now.getFullYear(), now.getMonth() + 2, 0)
    lastFriday = nextMonthLastDay
    while (lastFriday.getDay() !== 5) {
      lastFriday = new Date(lastFriday.getFullYear(), lastFriday.getMonth(), lastFriday.getDate() - 1)
    }
  }
  return Math.ceil((lastFriday.getTime() - now.getTime()) / (1000 * 60 * 60 * 24))
})
</script>
