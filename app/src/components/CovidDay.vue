<template>
    <router-link :to="covidPath" class="card">
      <h2> {{ stat.date_of_interest }}</h2>
    </router-link>
  </template>
  
  <script setup>
  import { computed } from "vue";
  const props = defineProps({
    stat: Object,
  });
  const covidPath = computed(() => {
    return `resource/rc75-m7u3.json`;
  });
  </script>
  
  <style scoped>
  .card {
    width: 28%;
    height: 80px;
    background-color: aliceblue;
    margin: 30px 0;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 10px;
    text-transform: uppercase;
  }
  img {
    width: 100%;
    height: 80%;
    object-fit: cover;
  }
  </style>