<script setup>
import Card from './Card.vue'
import Pagination from './Pagination.vue'
import { ref } from 'vue'

defineProps({
  items: Array,
  isFavorites: Boolean
})

const emit = defineEmits(['addToFavorite', 'addToCart'])



// Установите начальное количество товаров на странице и текущую страницу
const itemsPerPage = 4
const currentPage = ref(1)


// Метод для обработки события изменения страницы
const handlePageChange = (newPage) => {
  currentPage.value = newPage
}
</script>

<template>
  <div class="grid grid-cols-4 gap-5" v-auto-animate>
    <Card
      v-for="item in items"
      :key="item.id"
      :id="item.id"
      :title="item.title"
      :imageUrl="item.imageUrl"
      :price="item.price"
      :onClickFavorite="isFavorites ? null : () => emit('addToFavorite', item)"
      :onClickAdd="isFavorites ? null : () => emit('addToCart', item)"
      :isFavorite="item.isFavorite"
      :isAdded="item.isAdded"
    />
    <Pagination
      :items-per-page="itemsPerPage"
      :current-page="currentPage"
      @page-changed="handlePageChange"
    />
  </div>
</template>
