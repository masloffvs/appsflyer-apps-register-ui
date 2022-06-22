<template>
  <div>
    <error-alert :onClose="onClose" v-show="errorAlert"/>
    <success-alert :onClose="onClose" v-show="successAlert" :devKey="devKey"/>

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
                v-model="packageName"
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
            @click.prevent="checkAndRegisterApp(packageName)"
            type="submit"
            class="inline-flex justify-center py-2 px-4 border border-transparent shadow-sm text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500"
          >
            <svg v-if="stateLoading" class="animate-spin -ml-1 mr-3 h-5 w-5 text-white" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
              <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
              <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
            </svg>

            Получить AppsFlyer Key
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import axios from "axios";
import ErrorAlert from '../components/ErrorAlert.vue';
import SuccessAlert from '../components/SuccessAlert.vue';

export default defineComponent({
  components: { ErrorAlert, SuccessAlert },
  data() {
    return {
      packageName: "",
      errorAlert: false,
      successAlert: false,
     
      devKey: "",

      stateLoading: false
    }
  },
  methods: {
    checkAndRegisterApp(packageName: string) {      
      if (!this.stateLoading) {
        this.stateLoading = true

        axios({
          url: `http://appsflyer.wfc.su/api/appsflyer/app/registerAppInAppsflyer?packageName=${packageName}`,
          method: "GET"
        }).then(e => {
          if (e.data.success == false) {
            this.errorAlert = true
          } else if (e.data.success == true) {
            this.successAlert = true
            this.devKey = e.data.devKey
          }

        }).catch(e => {
            this.errorAlert = true
        }).finally(() => {
          this.stateLoading = false
        })
      }
    },

    onClose() {
      this.errorAlert = false
      this.successAlert = false
    }
  }
})
</script>
