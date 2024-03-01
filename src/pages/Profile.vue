<script>
import axios from 'axios'

export default {
  data() {
    return {
      login: '',
      password: '',
      email: '',
      phone: ''
    }
  },
  methods: {
    submitForm() {
      const formData = {
        login: this.login,
        password: this.password,
        email: this.email,
        phone: this.phone
      }

      axios
        .post('https://158f69488853fed3.mokky.dev/users', formData)
        .then((response) => {
          // обработка успешной отправки
          console.log(response.data)
        })
        .catch((error) => {
          // обработка ошибок при отправке
          console.error(error)
        })
    }
  }
}
</script>

<template>
  <div class="flex space-x-4">
    <div class="min-h-screen flex justify-center w-full">
      <div class="w-full max-w-lg mx-4">
        <h2 class="text-3xl font-bold text-center mb-6">Регистрация</h2>
        <div class="bg-white py-8 px-6 sm:rounded-lg">
          <form class="space-y-6" @submit.prevent="submitForm">
            <div>
              <input
                v-model="login"
                id="login"
                name="login"
                type="text"
                required
                class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
                placeholder="Логин"
              />
            </div>
            <div>
              <input
                v-model="password"
                id="password"
                name="password"
                type="password"
                required
                class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
                placeholder="Пароль"
              />
            </div>
            <div>
              <input
                v-model="email"
                id="email"
                name="email"
                type="email"
                required
                class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
                placeholder="Почта"
              />
            </div>
            <div>
              <input
                v-model="phone"
                id="phone"
                name="phone"
                type="tel"
                required
                class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500"
                placeholder="Телефон"
              />
            </div>
            <div class="flex items-center justify-end mt-4">
              <button
                type="submit"
                class="px-6 py-2 bg-indigo-600 text-white rounded-md hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-opacity-50"
              >
                Подтвердить
              </button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>
