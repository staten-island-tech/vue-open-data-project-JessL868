import { onMounted } from 'vue';
<template>
  <div>
    <h2>{{ pokemon.name }}</h2>
    <div class="abilities">
      <h5 v-for="stat in days" :key="stat">
        Case Count: {{ stat.case_count }} <br>
        Probable Case Count: {{ stat.probable_case_count }} <br>
        Hospitalized Count: {{ stat.hospitalized_count }} <br>
        Death Count: {{ stat.death_count }}
      </h5>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
const route = useRoute();
const days = ref("");
async function getData() {
  let res = await fetch(`https://data.cityofnewyork.us/resource/rc75-m7u3.json`);
  let data = await res.json();
  days.value = data;
}
onMounted(() => {
  getData();
});
</script>

<style scoped></style>