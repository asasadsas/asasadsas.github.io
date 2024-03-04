
<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input type="text" v-model="searchQuery" @input="getSearchResults" placeholder="Search for a city." class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]">
    </div>
  </main>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const APIkey = "54cd72cd0ad6469f189bea3e0914c199";
const searchQuery = ref("");
const queryTimeout = ref(null);
const searchResults = ref(null);

const getSearchResults = () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== '') {
      try {
        const result = await axios.get(`http://dataservice.accuweather.com/locations/v1/cities/search?apikey=0UURNw3jmJAcvLqYGLDI2OqBSpBHAWqC&q=${citySearch}`);
        searchResults.value = result.data;
        console.log(searchResults.value);
      } catch (error) {
        console.error("Error fetching data:", error);
      }
    } else {
      searchResults.value = null;
    }
  }, 300);
};
</script>