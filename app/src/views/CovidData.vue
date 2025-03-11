import { onMounted } from 'vue';
<template>
  <div>
    <h2>{{ day.date_of_interest }}</h2>
    <h5>
      Case Count: {{ day.case_count }} <br>
      Probable Case Count: {{ day.probable_case_count }} <br>
      Hospitalized Count: {{ day.hospitalized_count }} <br>
      Death Count: {{ day.death_count }}
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

<style scoped></style>