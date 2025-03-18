<template>
  <div class="container">
    <CovidDay
      v-for="(stat) in days"
      :key="stat.date_of_interest"
      :stat="stat"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import CovidDay from "../components/CovidDay.vue";
const days = ref("");
async function getData() {
  let res = await fetch("https://data.cityofnewyork.us/resource/rc75-m7u3.json?$limit=200");
  let data = await res.json();
  days.value = data;
}
onMounted(() => {
  getData();
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
</style>