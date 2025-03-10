<template>
  <div class="container">
    <div v-for="(person, index) in people" :key="index" :person="person" :id="index + 1">
      {{ person.pd_desc }}
    </div>
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue'
const people = ref([])

async function getPeople() {
  try {
    const response = await fetch('https://data.cityofnewyork.us/resource/uip8-fykc.json')
    let data = await response.json()
    people.value = data
    console.log(data)
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(() => {
  getPeople()
})
</script>

<style scoped></style>
