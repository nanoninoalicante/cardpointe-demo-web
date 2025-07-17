<template>
  <div class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-100">
    <!-- Header -->
    <header class="bg-white shadow-sm">
      <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="flex justify-between items-center py-6">
          <div class="flex items-center">
            <h1 class="text-2xl font-bold text-gray-900">CardPointe Demo</h1>
          </div>
          <div class="flex items-center space-x-4">
            <NuxtLink
              to="/docs"
              class="text-sm text-blue-600 hover:text-blue-800"
            >
              📚 Documentation
            </NuxtLink>
            <span class="text-sm text-gray-500">Test Environment</span>
            <div class="h-2 w-2 bg-green-400 rounded-full"></div>
          </div>
        </div>
      </div>
    </header>
    <!-- Main Content -->
    <main class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-12">
      <!-- Hero Section -->
      <div class="text-center mb-12">
        <h2 class="text-4xl font-bold text-gray-900 mb-4">
          Secure Payment Processing
        </h2>
        <p class="text-xl text-gray-600 max-w-2xl mx-auto mb-8">
          Experience CardPointe's hosted iframe tokenizer for secure,
          PCI-compliant payment processing
        </p>
        <NuxtLink
          to="/cardpointe"
          class="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700 transition-colors duration-200"
        >
          Try CardPointe Demo
        </NuxtLink>
      </div>


    </main>
  </div>
</template>

<script setup>
</script>