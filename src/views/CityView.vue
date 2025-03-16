<template>
  <div>
    <Suspense>
      <AsyncCityView />
      <template #fallback>
        <h1>Loading...</h1>
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from "../components/AsyncCityView.vue"
</script>