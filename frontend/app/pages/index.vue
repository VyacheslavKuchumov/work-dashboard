<template>
  <UContainer class="py-10 space-y-8">
    <UCard class="p-6 text-center">
      <h1 class="text-3xl font-bold mb-2">Workday Countdown</h1>
      <p v-if="isWorkday">{{ workdayTimeLeft }}</p>
      <p v-else class="text-green-500">Workday is over 🎉</p>
    </UCard>

    <UCard class="p-6 text-center">
      <h2 class="text-2xl font-bold mb-2">Days Until Paycheck</h2>
      <p>{{ daysUntilPaycheck }} days</p>
    </UCard>

    <UCard class="p-6 text-center">
      <h2 class="text-2xl font-bold mb-2">Days Until Pizza Party 🍕</h2>
      <p>{{ daysUntilPizzaParty }} days</p>
    </UCard>
  </UContainer>
</template>

<script setup lang="ts">
import { ref, computed, onMounted } from 'vue'

// Workday timer
const workdayTimeLeft = ref('')
const isWorkday = ref(false)

function updateWorkdayTimer() {
  const now = new Date()
  const day = now.getDay() // 0 = Sunday
  const start = new Date()
  start.setHours(10, 0, 0, 0)
  const end = new Date()
  end.setHours(19, 0, 0, 0)

  if (day >= 1 && day <= 5 && now >= start && now <= end) {
    isWorkday.value = true
    const diffMs = end.getTime() - now.getTime()
    const hours = Math.floor(diffMs / (1000 * 60 * 60))
    const minutes = Math.floor((diffMs % (1000 * 60 * 60)) / (1000 * 60))
    const seconds = Math.floor((diffMs % (1000 * 60)) / 1000)
    workdayTimeLeft.value = `${hours}h ${minutes}m ${seconds}s left`
  } else {
    isWorkday.value = false
  }
}

// Paycheck countdown (10th day of the month)
const daysUntilPaycheck = computed(() => {
  const now = new Date()
  let payday = new Date(now.getFullYear(), now.getMonth(), 10)
  if (now > payday) {
    payday = new Date(now.getFullYear(), now.getMonth() + 1, 10)
  }
  return Math.ceil((payday.getTime() - now.getTime()) / (1000 * 60 * 60 * 24))
})

// Pizza party countdown (last Friday of the month)
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

// Update workday timer every second
onMounted(() => {
  updateWorkdayTimer()
  setInterval(updateWorkdayTimer, 1000)
})
</script>
