<template>
  <header class="sticky top-0 bg-weather-primary shadow-lg">
    <nav
      class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6"
    >
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-3 cursor-pointer">
          <i class="fa-solid fa-gear text-2xl"></i>
          <p class="text-2xl">The Local Weather</p>
        </div>
      </RouterLink>

      <div class="flex gap-3 flex-1 justify-end">
        <i
          class="fa-solid fa-circle-info text-xl hover:text-weather-secondary duration-150 cursor-pointer" @click="toggleModel"
        >
        </i>
        <i class="fa-solid fa-circle-plus hover:text-weather-secondary duration-150 text-xl" >
        </i>
      </div>
      <BaseModel :modalActive="modalActive" @closeModal="toggleModel">
        <h1>你好，我是前端开发者Sy_</h1>
        <span>欢迎访问我的个人网站：</span>
        <a href="https://shenying.online" class="cursor-pointer hover:text-weather-primary duration-300 hover:underline">SHEN YING</a> <br>
      </BaseModel>
    </nav>
  </header>
</template>

<script setup>
import { ref } from "vue";
import { RouterLink } from "vue-router";
import BaseModel from './BaseModel.vue'

const modalActive = ref(false)
const toggleModel = () => {
  modalActive.value = !modalActive.value
}
</script>
