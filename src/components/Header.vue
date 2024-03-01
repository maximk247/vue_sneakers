<script setup>
import Modal from './Modal.vue'
import { ref } from 'vue'
const isModalOpen = ref(false)
const userLogin = ref('Профиль') // Начальное значение
// Method to toggle the modal
function toggleModal() {
  isModalOpen.value = !isModalOpen.value
}

defineProps({
  totalPrice: Number
})

const emit = defineEmits(['openDrawer'])

function handleLoginSuccess(login) {
  userLogin.value = login;
  isModalOpen.value = false; // Закрыть модальное окно после успешного входа
}
</script>

<template>
  <header class="flex justify-between border-b border-slate-200 px-10 py-8">
    <router-link to="/"
      ><div class="flex items-center gap-4">
        <img src="/logo.png" alt="Logo" class="w-10" />
        <div>
          <h2 class="text-xl font-bold uppercase">Sneakers</h2>
          <p class="text-slate-400">Магазин лучших кроссовок</p>
        </div>
      </div></router-link
    >

    <ul class="flex items-center gap-10">
      <li
        @click="() => emit('openDrawer')"
        class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black"
      >
        <img src="/cart.svg" alt="Cart" />
        <b>{{ totalPrice }} руб.</b>
      </li>

      <router-link to="/favorites">
        <li class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black">
          <img src="/heart.svg" alt="Cart" />
          <span>Закладки</span>
        </li>
      </router-link>

      <li
        @click="toggleModal"
        class="flex items-center cursor-pointer gap-3 text-gray-500 hover:text-black"
      >
        <img src="/profile.svg" alt="Cart" />
        <span>{{ userLogin }}</span>
      </li>
    </ul>
    <Modal v-if="isModalOpen" @close="toggleModal" @loginSuccess="handleLoginSuccess"> </Modal>
  </header>
</template>
