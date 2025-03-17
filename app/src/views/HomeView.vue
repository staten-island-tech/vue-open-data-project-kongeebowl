<template>
  <div class="container items-center justify-center flex flex-col m-auto">
    <div
      v-for="(person, index) in people"
      :key="index"
      :person="person"
      :id="index + 1"
      class="card w-full sm:w-[90%] md:w-[80%] lg:w-[75%] h-auto rounded-3xl flex flex-col items-center justify-between bg-blue-200 text-center p-2 shadow-sm m-5"
    >
      {{ perp }}
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
