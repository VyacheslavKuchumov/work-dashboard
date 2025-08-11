<template>
  <UCard 
        variant="soft"
        class="bg-white shadow-lg rounded-lg overflow-hidden"
        :ui="{
        header: 'p-0 sm:px-0', // Remove padding from header slot
        }">
        <template #header>
            <NuxtImg
            src="/images/money.jpg"
            alt="Paycheck Countdown"
            class="w-full h-62 object-cover rounded-t-lg"
            />
        </template>
        <p class="text-xl">Days until paycheck:</p>
        <p class="text-2xl font-semibold">{{ daysUntilPaycheck }} days</p>
  </UCard>
</template>

<script setup lang="ts">


const daysUntilPaycheck = computed(() => {
  const now = new Date()
  let payday = new Date(now.getFullYear(), now.getMonth(), 10)
  if (now > payday) {
    payday = new Date(now.getFullYear(), now.getMonth() + 1, 10)
  }
  return Math.ceil((payday.getTime() - now.getTime()) / (1000 * 60 * 60 * 24))
})
</script>
