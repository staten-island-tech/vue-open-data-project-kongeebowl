<template>
  <div class="container m-auto w-1/2 h-1/2">
    <Pie :data="chartData" :options="chartOptions" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { Pie } from 'vue-chartjs'
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
  RadialLinearScale,
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, ArcElement, CategoryScale, RadialLinearScale)

const chartData = ref({
  labels: [],
  datasets: [
    {
      data: [],
      backgroundColor: ['red', 'blue', 'yellow'],
      hoverOffset: 4,
    },
  ],
})

const chartOptions = ref({
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Pie Chart Example',
    },
    tooltip: {
      enabled: true,
    },
  },
  aspectRatio: 1,
  layout: {
    padding: 20,
  },
  legend: {
    position: 'top',
    labels: {
      font: {
        size: 14,
      },
    },
  },
})

onMounted(async () => {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json?$limit=100')
    const data = await response.json()
    const crimeCounts = {}
    data.forEach((item) => {
      const crime = item.pd_desc
      crimeCounts[crime] = (crimeCounts[crime] || 0) + 1
    })

    chartData.value = {
      labels: Object.keys(crimeCounts),
      datasets: [
        {
          data: Object.values(crimeCounts),
          backgroundColor: ['red', 'blue', 'green', 'orange', 'purple'],
          hoverOffset: 4,
        },
      ],
    }
  } catch (error) {
    console.error('Error fetching data:', error)
  }
})
</script>

<style scoped></style>
