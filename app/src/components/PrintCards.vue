<template>
  <div>
    <div>
      {{ person.perp_race }}
      {{ person.pd_desc }}
      <img
        src="https://static.wikia.nocookie.net/nopixel/images/e/ec/Timcheese.png.png/revision/latest?cb=20250305065848"
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
