<template>
      <div class="d-flex justify-content-end mb-3 mt-5">
  <div class="mx-3">
  Price:
  <button  v-if="(sortBy =='price' && sortDirection =='asc')"   @click="sortData('price', 'dsc')"> Descending</button>
  <button v-else @click="sortData('price', 'asc')"> Ascending</button>
  </div>
  <div class="mx-3">
  Rating: 
  <button v-if="(sortBy =='rating' && sortDirection =='asc')"   @click="sortData('rating', 'dsc')"> Descending</button>
  <button v-else  @click="sortData('rating', 'asc')"> Ascending</button>
  </div>
  </div>
</template>

<script setup>
const props = defineProps(
    [  "sortBy","sortDirection","sortData"]
)
</script>

<style scoped>

</style>