<template>
  <router-link :to="chartPath" class="button">
    <h3>Total Deaths Chart</h3>
  </router-link>
  <br>
  <div class="container">
    <CovidDay
      v-for="(stat) in days"
      :key="stat.date_of_interest"
      :stat="stat"
    />
  </div>
</template>

<script setup>
import { ref, onMounted, computed } from "vue";
import CovidDay from "../components/CovidDay.vue";
const days = ref("");
async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/rc75-m7u3.json?$limit=50");
  let data = await res.json();
  days.value = data;
}
onMounted(() => {
  getData();
});
const chartPath = computed(() => {
    return `/chart`
});
</script>

<style scoped>
.container {
  width: 90vw; 
  max-width: 1200px; 
  margin: 30px auto;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center; 
  gap: 20px; 

}
.button {
  display: inline-block; 
  border-radius: 8px; 
  border: 1px solid #b2ebf2; 
  background-color: #e0f2f7; 
  color: #333;
  height: auto; 
  width: auto; 
  padding: 10px 20px; 
  text-align: center;
  text-decoration: none; 
  font-size: 1rem;
  transition: background-color 0.3s ease; 
  margin-bottom: 20px; 
}
.button:hover {
  background-color: #e4eef9;
}
h3 {
  margin: 0; 
  font-size: 1.2rem;
}
</style>