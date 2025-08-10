<!-- app.vue -->
<template>
  <UApp>
    <!-- Main layout container -->
    <div class="min-h-screen flex flex-col bg-gray-50 text-gray-900">
      <!-- Header -->
      <header class="bg-white border-b border-gray-200 shadow-sm">
        <nav class="container mx-auto flex items-center justify-between py-4 px-6">
          <h1 class="text-xl font-bold">⏳ Workday Timer</h1>
          <div class="flex gap-4">
            <UButton to="/" variant="soft" color="primary">Home</UButton>
            <UButton to="/about" variant="soft" color="primary">About</UButton>
          </div>
        </nav>
      </header>

      <!-- Page Content -->
      <main class="flex-1 container mx-auto p-6">
        <NuxtPage />
      </main>

      <!-- Footer -->
      <footer class="bg-white border-t border-gray-200 py-4 text-center text-sm text-gray-500">
        © {{ new Date().getFullYear() }} Sluvik Developments. All rights reserved.
      </footer>
    </div>
  </UApp>
</template>

<script setup>
// Nuxt UI auto-imports components like UApp, UButton, etc.
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
}
</style>
