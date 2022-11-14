<template>
    <div v-for="city in savedCity" :key="city.id">
        <CityCard/>
    </div>
</template>

<script setup lang="ts">
import axios from 'axios';
import CityCard from './CityCard.vue';


const savedCity: any = []
const getcity = async () => {
    if (localStorage.getItem("savedCity")) {
        savedCity.value = JSON.parse(localStorage.getItem("savedCity") || "")

        const requests: any = []

        savedCity.value.forEach((city: { coords: { lat: number; lng: number; }; }) => {
            requests.push(
                axios.get(
                    `https://api.openweathermap.org/data/2.5/weather?lat=${city.coords.lat}&lon=${city.coords.lng}&appid=7efa332cf48aeb9d2d391a51027f1a71&units=metric`
                )
            )
        });

        const weatherData = await Promise.all(requests);

        weatherData.forEach((value, index) => {
            savedCity.value[index].weather = value.data;
        });
    }
}
await getcity()


</script>

<style scoped>

</style>