<script setup lang="ts">
import {onMounted, ref} from 'vue';
import L from 'leaflet'

const lat = ref<number | null>(null);
const long = ref<number | null>(null);
const mapContainer = ref()

const getLocation = async () => {
  if(navigator.geolocation) {

    navigator.geolocation.watchPosition((location) => {
      lat.value = location.coords.latitude;
      long.value = location.coords.longitude;
    })
  }
}

onMounted(() => {
  var map = L.map(mapContainer.value).setView([51.505, -0.09], 13);
  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
}).addTo(map);
})
</script>

<template>
  <div>
    <button @click="getLocation">
      Get Location
    </button>
    <p>{{ lat }}</p>
    <p>{{ long }}</p>

    <div ref="mapContainer" style="width: 800px; height: 600px;"></div>
  </div>
  
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
