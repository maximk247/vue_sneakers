<script>
import axios from 'axios'
export default {
  name: 'Modal',
  data() {
    return {
      isModalOpen: true,
      email: '',
      phone: ''
    }
  },
  mounted() {
    document.body.style.overflow = this.isModalOpen ? 'hidden' : ''
  },
  watch: {
    isModalOpen(newVal) {
      document.body.style.overflow = newVal ? 'hidden' : ''
    }
  },
  beforeUnmount() {
    document.body.style.overflow = ''
  },
  methods: {
    close() {
      this.$emit('close')
      document.body.style.overflow = ''
    },
    toggleModal() {
      this.isModalOpen = !this.isModalOpen
    },
    login() {
      axios
        .get('https://158f69488853fed3.mokky.dev/users')
        .then((response) => {
          // Предполагаем, что сервер возвращает массив объектов пользователей
          const users = response.data
          console.log(users)
          const user = users.find((u) => u.email === this.email && u.phone === this.phone)
          if (user) {
            this.$emit('loginSuccess', user.login) // Посылает событие с логином пользователя
            this.close()
          } else {
            console.error('User not found or phone incorrect')
          }
          this.$emit('close')
        })
        .catch((error) => {
          console.error('Error during login:', error)
        })
    }
  }
}
</script>

<template>
  <transition name="modal-fade">
    <div
      class="fixed inset-0 bg-gray-600 bg-opacity-50 z-50 flex justify-center items-center px-4"
      v-if="isModalOpen"
    >
      <div class="bg-white p-6 rounded-lg max-w-sm w-full">
        <div class="flex justify-between items-center mb-4">
          <h3 class="text-lg font-bold w-full text-center pl-12.5px uppercase">Войти</h3>
          <button @click="close" class="text-lg font-semibold text-gray-500 hover:text-gray-700">
            &times;
          </button>
        </div>
        <form class="space-y-4" @submit.prevent="login">
          <div>
            <input
              v-model="email"
              type="email"
              id="email"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500"
              placeholder="Почта"
            />
          </div>
          <div>
            <input
              v-model="phone"
              type="phone"
              id="phone"
              class="mt-1 block w-full px-3 py-2 border border-gray-300 rounded-md shadow-sm placeholder-gray-400 focus:outline-none focus:ring-1 focus:ring-blue-500 focus:border-blue-500"
              placeholder="Номер телефона"
            />
          </div>
          <div class="flex items-center justify-between pt-4">
            <router-link to="/profile">
              <button
                type="button"
                @click="close"
                class="px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-gray-700 bg-gray-100 hover:bg-gray-200"
              >
                Создать новый аккаунт
              </button>
            </router-link>

            <button
              type="submit"
              class="px-4 py-2 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-blue-600 hover:bg-blue-700"
            >
              Войти
            </button>
          </div>
        </form>
      </div>
    </div>
  </transition>
</template>
