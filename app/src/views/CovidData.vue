import { onMounted } from 'vue';
<template>
  <div >
    <h2 v-for="(stat) in day" :key="stat.date_of_interest"
    :stat="stat">{{ stat.date_of_interest }}</h2>
    <h5 v-for="(stat) in day" :key="stat.date_of_interest"
    :stat="stat">
      Case Count: {{ stat.case_count }} <br>
      Probable Case Count: {{ stat.probable_case_count }} <br>
      Hospitalized Count: {{ stat.hospitalized_count }} <br>
      Death Count: {{ stat.death_count }}
    </h5>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
const route = useRoute();
const day = ref("");
async function getData() {
  let res = await fetch(`https://data.cityofnewyork.us/resource/rc75-m7u3.json?date_of_interest=${route.params.date_of_interest}`);
  let data = await res.json();
  day.value = data;
}
onMounted(() => {
  getData();
});
</script>

<style scoped>
h2 {
  text-align: center;
  font-size: 2.5rem;
  margin-bottom: 15px;
  width: 100%;
  margin-left: 20rem;
}

h5 {
  font-size: 1rem;
  text-align: center;
  margin-bottom: 10px;
  width: 80%;
  margin-left: 23rem;
}

h5 br {
  margin-bottom: 5px;
}

</style>