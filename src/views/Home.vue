<template>
  <div>
    <div class="max-w-7xl mx-auto py-12 px-4 sm:px-6 lg:py-16 lg:px-8 lg:flex lg:items-center lg:justify-between">
      <h2 class="text-3xl font-extrabold tracking-tight text-gray-900 sm:text-4xl">
        <span class="block">Нужен AppsFlyer Key для твоего приложения?</span>
        <span class="block text-indigo-600">Получи его прямо сейчас.</span>
      </h2>
    </div>

    <div class="mt-6">
      <div class="shadow sm:rounded-md sm:overflow-hidden">
        <div class="px-4 py-5 bg-white space-y-6 sm:p-6">
          <div>
            <label
              for="package"
              class="block text-sm font-medium text-gray-700 mb-2"
            >
              Введите пакет приложения
            </label>

            <div class="mt-1 relative rounded-md shadow-sm">
              <input
                id="package"
                type="text"
                name="package"
                class="focus:ring-indigo-500 focus:border-indigo-500 block w-full pl-4 pr-4 sm:text-sm border-gray-300 rounded-md"
                placeholder="com.example.application"
              >
            </div>
          </div>
        </div>

        <div class="px-4 py-3 bg-gray-50 text-right sm:px-6">
          <button
            type="submit"
            class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            Получить AppsFlyer Key
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

import HelloWorld from '../components/HelloWorld.vue'

export default defineComponent({
  components: {},
})
</script>
