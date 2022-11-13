<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input v-model="searchQuery" @input="getSearchResults" type="text" placeholder="Search by city/state"
        class="p-2 w-full bg-transparent border-b focus:border-color-secondary focus:outline-none focus:shadow-sm">
      <ul v-if="mapboxSearchResults" class="absolute bg-color-secondary w-full shadow-md p-2 top-[66px] rounded-lg">
        <p v-if="searchError">Sorry, something quiet wrong, please try again</p>
        <p v-if="!searchError && mapboxSearchResults == 0">No result found, please try others location</p>
        <template v-else>
          <li v-for="searchResult in mapboxSearchResults" :key="searchResult['id']" class="py-1 cursor-pointer">
            {{ searchResult['place_name'] }}
          </li>
        </template>
      </ul>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import axios from 'axios';

const searchQuery = ref("")
const queryTimeout = ref()
const mapboxAPIkey = "pk.eyJ1Ijoiam9obmtvbWFybmlja2kiLCJhIjoiY2t5NjFzODZvMHJkaDJ1bWx6OGVieGxreSJ9.IpojdT3U3NENknF6_WhR2Q"
const mapboxSearchResults = ref(null)
const searchError = ref()

const getSearchResults = () => {
  clearTimeout(queryTimeout.value)
  queryTimeout.value = setTimeout(async () => {
    if (searchQuery.value !== "") {
      try {
        const result = await axios.get(`https://api.mapbox.com/geocoding/v5/mapbox.places/${searchQuery.value}.json?access_token=${mapboxAPIkey}&type=place`)
        mapboxSearchResults.value = result.data.features
        console.log(mapboxSearchResults.value)
      } catch{
        searchError.value = true
      }
      return
    } mapboxSearchResults.value = null
  }, 300);
}
</script>

