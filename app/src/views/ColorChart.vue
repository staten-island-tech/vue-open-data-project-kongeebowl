<template>
  <div class="container m-auto w-3/5 h-3/5">
    <PieChart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import PieChart from '@/components/PieChart.vue'
import { onMounted, ref } from 'vue'

const chartData = ref({
  labels: [],
  datasets: [
    {
      backgroundColor: ['red', 'blue', 'yellow'],
      data: [],
    },
  ],
})

const chartOptions = ref({
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Races of Perpetrators',
      font: {
        size: 20,
      },
      color: '#FFFFF0',
    },
    legend: {
      position: 'top',
      labels: {
        color: '#FFFFF0',
      },
    },
    tooltip: {
      titleColor: '#FFFFF0',
      bodyColor: '#FFFFF0',
    },
  },
  aspectRatio: 1,

  legend: {
    position: 'top',
    labels: {
      font: {
        size: 14,
      },
    },
  },
})

async function getPeople() {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json')
    const data = await response.json()

    const raceCounts = {}
    data.forEach((person) => {
      const race = person.perp_race
      raceCounts[race] = (raceCounts[race] || 0) + 1
    })

    chartData.value = {
      labels: Object.keys(raceCounts),
      datasets: [
        {
          backgroundColor: ['red', 'blue', 'green', 'orange', 'purple', 'yellow', 'cyan'],
          data: Object.values(raceCounts),
        },
      ],
    }
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  getPeople()
})
</script>

<style scoped></style>
