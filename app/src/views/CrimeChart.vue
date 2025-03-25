<template>
  <div>
    <div class="text-center container m-auto">
      <label for="boro-select" class="text-[#FFFFF0] mx-2">Choose a Borough:</label>
      <select
        v-model="boroughs"
        id="boro-select"
        @change="getPeople"
        class="text-[#FFFFF0] bg-[#3d3637]"
      >
        <option value="all" selected>All</option>
        <option value="S">Staten Island</option>
        <option value="B">Brooklyn</option>
        <option value="M">Manhattan</option>
        <option value="Q">Queens</option>
        <option value="K">Bronx</option>
      </select>
    </div>
    <div class="container m-auto w-3/5 h-3/5">
      <DonutChart :data="chartData" :options="chartOptions" />
      <br />
      <p class="text-center m-auto text-[#fff8a5] my-20 text-2xl">
        Crimes Comitted In This Borough: {{ crimesComitted }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import DonutChart from '@/components/DonutChart.vue'

const chartData = ref({
  labels: [],
  datasets: [
    {
      data: [],
      backgroundColor: ['red', 'blue', 'yellow'],
    },
  ],
})

const chartOptions = ref({
  responsive: true,
  plugins: {
    title: {
      display: true,
      text: 'Crimes Committed',
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

const boroughs = ref('all')
const crimesComitted = ref('')

async function getPeople() {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json')
    const data = await response.json()

    const crimeCounts = {}

    if (boroughs.value === 'all') {
      data.forEach((person) => {
        const crime = person.ofns_desc
        crimeCounts[crime] = (crimeCounts[crime] || 0) + 1
      })
      crimesComitted.value = data.length
    } else {
      const filteredPeople = data.filter((person) => person.arrest_boro === boroughs.value)
      crimesComitted.value = filteredPeople.length
      filteredPeople.forEach((person) => {
        const crime = person.ofns_desc
        crimeCounts[crime] = (crimeCounts[crime] || 0) + 1
      })
    }

    chartData.value = {
      labels: Object.keys(crimeCounts),
      datasets: [
        {
          backgroundColor: [
            '#FF5733',
            '#33FF57',
            '#3357FF',
            '#FF33A1',
            '#F4D03F',
            '#1F77B4',
            '#8E44AD',
            '#F39C12',
            '#C0392B',
            '#16A085',
            '#27AE60',
            '#2980B9',
            '#8E44AD',
            '#9B59B6',
            '#34495E',
            '#E67E22',
            '#F1C40F',
            '#2ECC71',
            '#3498DB',
            '#9B59B6',
            '#1ABC9C',
            '#D35400',
            '#7F8C8D',
            '#BDC3C7',
            '#FF8C00',
            '#6C3483',
            '#D32F2F',
            '#0288D1',
            '#7B1FA2',
            '#FF1744',
            '#00E5FF',
            '#FF4081',
            '#64FFDA',
            '#8D6E63',
            '#00C853',
            '#C2185B',
            '#7C4DFF',
            '#2196F3',
            '#009688',
            '#FF5722',
            '#CDDC39',
            '#FFEB3B',
            '#9E9E9E',
            '#FF9800',
            '#3F51B5',
            '#0097A7',
            '#FFB300',
            '#7B1FA2',
            '#FF6F00',
            '#2E7D32',
            '#0288D1',
            '#5C6BC0',
            '#512DA8',
            '#4CAF50',
            '#FF5252',
            '#009688',
            '#FF4081',
            '#009688',
            '#795548',
            '#8D6E63',
            '#E57373',
            '#C62828',
          ],
          data: Object.values(crimeCounts),
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
