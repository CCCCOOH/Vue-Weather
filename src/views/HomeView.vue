<template>
  <main class="container text-white">
    <div type="text" class="pt-4 mb-8 relative">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search for a city or state...(such as 650100)"
        class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
        @input="getSearchResults"
      />
      <ul
        v-if="searchResults"
        class="absolute bg-weather-secondary text-white w-full shadow-md shadow-md py-2 px-1 top-[66px]"
      >
        <p v-if="searchError">Sorry, something went wrong, please try again.</p>
        <p v-if="!searchError && searchResults.length === 0 || searchResults[0].length === 0">No results match your query, try a different term.</p>
        <template v-else>
          <li class="cursor-pointer" v-for="searchResult in searchResults" :key="searchResult.adcode" @click="previewCity(searchResult)">
            {{ searchResult.city }}
          </li>
        </template>
      </ul>
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";
import { useRouter } from "vue-router"

const router = useRouter();

const apiKey = ref("51466edcbb25f717840d52b5bc19842e");
const searchQuery = ref("");
const queryTimeout = ref(null);
const searchResults = ref(null);
const searchError = ref(null);


const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(
          `https://restapi.amap.com/v3/weather/weatherInfo?key=${apiKey.value}&city=${searchQuery.value}`
        );
        searchResults.value = result.data.lives;
        //TODO 打印
        console.log(searchResults.value);
        return;
      } catch {
        searchError.value = true;
      }
    }
    searchResults.value = null;
  }, 300);
};

const previewCity = (searchResult) => {
  const { city, province, adcode } = searchResult;
  
  router.push({
    name: 'cityView',
    params: {
      province,
      city,
    },
    query: {
      preview: true,
      adcode
    }
  })
}
</script>
