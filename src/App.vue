<script setup lang="ts">
import {onMounted, ref} from 'vue';
import L from 'leaflet'

const lat = ref<number | null>(null);
const long = ref<number | null>(null);
const map = ref()
const mapContainer = ref()

const getLocation = async () => {
  if(navigator.geolocation) {

    let marker: L.Marker | null = null;

    navigator.geolocation.watchPosition((location) => {
      lat.value = location.coords.latitude;
      long.value = location.coords.longitude;
      map.value.setView([lat.value,long.value, 13]);

      if(!marker) {
        marker = L.marker([lat.value, long.value], {draggable: true})
          .addTo(map.value)
          .on("dragend", (event: L.DragEndEvent) => {
            console.log(event)
          });
      } else {
        marker.setLatLng([lat.value, long.value]);
      }
    })
  }
}

onMounted(() => {
  map.value = L.map(mapContainer.value).setView([-6.2390957, 106.7527616,], 13);
  L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
    maxZoom: 19,
    attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap</a>'
}).addTo(map.value);
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

</style>
