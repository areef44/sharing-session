<script setup lang="ts">
import {ref} from 'vue';

const lat = ref<number | null>(null);
const long = ref<number | null>(null);

const getLocation = async () => {
  if(navigator.geolocation) {

    navigator.geolocation.watchPosition((location) => {
      lat.value = location.coords.latitude;
      long.value = location.coords.longitude;
    })
  }
}
</script>

<template>
  <div>
    <button @click="getLocation">
      Get Location
    </button>
    <p>{{ lat }}</p>
    <p>{{ long }}</p>
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
