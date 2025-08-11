<template>
  <UCard
        variant="soft" 
        class="text-center bg-white shadow-lg rounded-lg overflow-hidden"
        :ui="{
        header: 'p-0 sm:px-0',
        }">
        <template #header>
            <NuxtImg 
            src="/images/chill.jpg"
            alt="Work is over"
            class="w-full h-full object-cover rounded-t-lg"
            />
        </template>
    <h1 class="text-3xl font-bold mb-2">Workday Countdown</h1>
    <p v-if="isWorkday">{{ workdayTimeLeft }}</p>
    <p v-else class="text-green-500">Workday is over 🎉</p>
  </UCard>
</template>

<script setup>


const workdayTimeLeft = ref('')
const isWorkday = ref(false)

function updateWorkdayTimer() {
  const now = new Date()
  const day = now.getDay()
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

onMounted(() => {
  updateWorkdayTimer()
  setInterval(updateWorkdayTimer, 1000)
})
</script>
