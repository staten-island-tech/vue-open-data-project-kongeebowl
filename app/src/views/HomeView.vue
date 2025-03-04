<template>
  <div class="container">
    <PokemonCards
      v-for="(pkmn, index) in pokemon.results"
      :key="index"
      :pokemon="pkmn"
      :id="index + 1"
    >
    </PokemonCards>
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue'
import PokemonCards from '../components/PokemonCards.vue'
const pokemon = ref('')

async function getPokemon() {
  const response = await fetch('https://pokeapi.co/api/v2/pokemon/?limit=151')
  let data = await response.json()
  pokemon.value = data
}
onMounted(() => {
  getPokemon()
})
</script>

<style scoped></style>
