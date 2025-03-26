<template>
  <div>
    <div>
      {{ person.perp_race }}
      {{ person.pd_desc }}
      <img
        src="https://m.media-amazon.com/images/I/714-7Eu91wL._AC_UF1000,1000_QL80_.jpg"
        alt="trumpy"
      />
      {{ person.perp_sex }}
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  person: Object,
})
</script>

<style scoped></style>
