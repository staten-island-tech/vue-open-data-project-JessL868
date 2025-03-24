<template>
    <router-link :to="covidPath" class="card">
      <h2>  {{ stat.date_of_interest }}</h2>
    </router-link>
  </template>
  
  <script setup>
  import { computed } from "vue";
  const props = defineProps({
    stat: Object,
    date_of_interest: String
  });
  const covidPath = computed(() => {
    return `/covid/${props.stat.date_of_interest}`;
  });
  </script>
  
  <style scoped>
  .card {
  width: calc(33.33% - 3-px);
  min-height: 100px; 
  background-color: #e0f2f7; 
  margin: 15px; 
  display: flex;
  flex-direction: column;
  justify-content: center; 
  align-items: center;
  padding: 15px;
  text-transform: uppercase;
  border-radius: 10px; 
  border: 1px solid #b2ebf2; 
  box-shadow: 2px 2px 5px rgba(0, 0, 0, 0.05); 
  text-decoration: none; 
  color: #333;
  transition: transform 0.2s ease-in-out; 
}

.card:hover {
  transform: scale(1.02); 
  box-shadow: 3px 3px 7px rgba(0, 0, 0, 0.1); 
  background-color: #e0ebf7; 
}
h2 {
  margin: 0; 
  font-size: 1.2rem;
  text-align: center; 
}
  </style>