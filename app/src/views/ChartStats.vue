<template>
    <div style="width: 70vw; height: 70vw; margin-top: 8rem;"><canvas id="covid"></canvas></div>
</template>

<script type="module" setup>
import Chart from 'chart.js/auto'
import { ref, onMounted } from "vue";
const days = ref("");
async function getData() {
    let res = await fetch("https://data.cityofnewyork.us/resource/rc75-m7u3.json?$limit=50");
    let data = await res.json();
    days.value = data;
}
onMounted(async () => {
    await getData();
    new Chart(
      document.getElementById('covid'),
      {
        type: 'bar',
        data: {
          labels: days.value.map(row => row.date_of_interest),
          datasets: [
            {
             label: 'Deaths by day',
             data: days.value.map(row => row.death_count)
             }
         ]
        },
        options: {
            plugins: {
                title: {
                    display: true,
                    text: 'Covid Deaths'
                }
            }
        }
      }
    );
});

</script>