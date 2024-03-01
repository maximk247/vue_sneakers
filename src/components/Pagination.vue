<script setup>
import { computed } from 'vue'

defineProps({
  currentPage: Number,
  itemsPerPage: Number,
  pageChanged: Function
})

const emit = defineEmits(['pageChanged'])

const totalPages = computed(() => {
  return 3
})

const goToPage = (page) => {
  console.log(page)
  if (page >= 1 && page <= totalPages.value) {
    emit('pageChanged', page)
  }
}

const pages = computed(() => {
  let pages = []
  for (let i = 1; i <= totalPages.value; i++) {
    pages.push(i)
  }
  return pages
})
</script>

<template>
  <nav class="flex items-center justify-center space-x-2">
    <button
      @click="goToPage(currentPage - 1)"
      :disabled="currentPage <= 1"
      class="rounded p-2 disabled:bg-gray-200"
    >
      &larr;
    </button>
    <button
      v-for="page in pages"
      :key="page"
      @click="goToPage(page)"
      :class="[
        'rounded p-2',
        {
          'bg-blue-600 text-white': page === currentPage,
          'bg-white text-black': page !== currentPage
        }
      ]"
    >
      {{ page }}
    </button>
    <button
      @click="goToPage(currentPage + 1)"
      :disabled="currentPage === totalPages"
      class="rounded p-2 disabled:bg-gray-200"
    >
      &rarr;
    </button>
  </nav>
</template>
