<template>
  <div>
    <div>
      {{ person.perp_race }}
      {{ person.pd_desc }}
      <img
        src="https://static.wikia.nocookie.net/nopixel/images/d/da/Timycheese.png.png/revision/latest/scale-to-width-down/250?cb=20250305081122"
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
