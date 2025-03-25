<template>
  <div class="container m-auto w-3/5 h-3/5">
    <BarChart :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import BarChart from '@/components/BarChart.vue'
import { onMounted, ref } from 'vue'

const chartData = ref({
  labels: [],
  datasets: [
    {
      label: 'Borough Count',
      backgroundColor: '#FDD835',
      data: [],
    },
  ],
})

const chartOptions = ref({
  scales: {
    y: {
      ticks: {
        color: '#FFFFF0',
      },
      grid: {
        color: '#6c5756',
      },
    },
    x: {
      ticks: {
        color: '#FFFFF0',
      },
      grid: {
        color: '#6c5756',
      },
    },
  },
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Arrests in Each Borough',
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
  elements: {
    bar: {
      borderWidth: 2,
    },
  },
  backgroundColor: '#3d3637',
})

async function getPeople() {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json')
    const data = await response.json()

    const boroCount = {}
    data.forEach((person) => {
      const boro = person.arrest_boro
      boroCount[boro] = (boroCount[boro] || 0) + 1
    })

    chartData.value = {
      labels: Object.keys(boroCount),
      datasets: [
        {
          label: 'Borough Chart',
          backgroundColor: '#FDD835',
          data: Object.values(boroCount),
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
