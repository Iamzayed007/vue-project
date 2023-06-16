<template>
  <div class="pagination">
    <div v-for="index in count" :key="index">
      <button
        @click="currentPage(index)"
        :class="[
          index == activePage ? 'btn btn-success' : 'btn btn-outline-success',
          'mx-1',
        ]"
      >
        {{ index }}
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, toRef, defineProps } from "vue";

defineProps({ count: Number, activePage: Number });

const emit = defineEmits(["current-page"]);

const currentPage = (index) => {
 
  emit("current-page", index);
};
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
}
</style>
