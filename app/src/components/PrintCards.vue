<template>
  <div>
    <div>
      {{ person.perp_race }}
      {{ person.pd_desc }}
      <img
        src="https://dims.apnews.com/dims4/default/d568bd0/2147483647/strip/true/crop/1621x1080+149+0/resize/599x399!/quality/90/?url=https%3A%2F%2Fassets.apnews.com%2F61%2F10%2Fc02e5570477abbc1d969e97bfece%2Funtitled-design-4.png"
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
