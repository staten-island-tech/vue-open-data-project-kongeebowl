<template>
  <div>
    <div>
      {{ person.perp_race }}
      {{ person.pd_desc }}
      <img
        src="https://www.google.com/imgres?q=Jamarius%20Quangle-Dangle&imgurl=https%3A%2F%2Fstatic.wikia.nocookie.net%2Famongusfan22%2Fimages%2Fa%2Fa3%2F6th-grader-leader-current.png%2Frevision%2Flatest%2Fthumbnail%2Fwidth%2F360%2Fheight%2F360%3Fcb%3D20231113021343&imgrefurl=https%3A%2F%2Famongusfan22.fandom.com%2Fwiki%2FJamarius_Quangledangle&docid=ZLYnFEEO5W_mwM&tbnid=tasHIbM5KdkpaM&vet=12ahUKEwjPzZCv76eMAxXjg4kEHdsxHTUQM3oECBMQAA..i&w=200&h=360&hcb=2&ved=2ahUKEwjPzZCv76eMAxXjg4kEHdsxHTUQM3oECBMQAA"
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
