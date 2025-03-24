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
  width: 80vw;
  margin: 30px auto;
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
  justify-content: space-around;
}
.button {
  border-radius: 10px;
  border-color: rgb(201, 201, 250);
  background-color: aliceblue;
  height: 2rem;
  width: 10rem;
  margin-left: -10rem;
}
</style>