<template>
  <tbody v-for="(d, index) in dataPaginated" :key="d.id">
    <tr class="border border-dark">
      <td class="border border-dark">{{ index + 1 }}</td>
      <td class="border border-dark">{{ d.title }}</td>
      <td class="border border-dark">{{ d.rating }}</td>
      <td class="border border-dark">{{ d.price }}</td>
      <td
        v-if="selectedProductId != d.id"
        class="border border-dark buttonClass"
      >
        <button class="btn text-sm-center" @click="toggleDetails(d.id)">
          Show
        </button>
      </td>
      <td
        v-if="selectedProductId == d.id"
        class="border border-dark closeButtonClass"
      >
        <button class="btn text-sm-center" @click="hideDetails">Close</button>
      </td>
    </tr>
    <tr v-if="selectedProductId == d.id">
      <td colspan="5">
        <ViewDetails :selectedProduct="selectedProduct" :loading="loading" />
      </td>
    </tr>
  </tbody>
</template>

<script setup>
import { ref, defineProps, defineEmits, provide } from "vue";
import ViewDetails from "./ViewDetails.vue";
import axios from "axios";
const props = defineProps(["data", "dataPaginated"]);
const selectedProductId = ref(null);
const selectedProduct = ref(null);
const loading = ref(true);

function toggleDetails(userId) {
  if (selectedProductId === userId) {
    hideDetails();
  } else {
    selectedProductId.value = userId;
    fetchUserDetails(userId);
  }
}

const fetchUserDetails = async (userId) => {
  try {
    const response = await axios.get(
      `https://dummyjson.com/products/${userId}`
    );
    selectedProduct.value = response.data;
    loading.value = false;
 
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

function hideDetails() {
  selectedProductId.value = null;
  selectedProduct.value = null;
}
</script>

<style scoped>
.buttonClass {
  display: flex;
  justify-content: center;
  align-content: center;
  border: none !important ;
}
.buttonClass .btn {
  background-color: rgb(83, 157, 46);
  color: white;
  padding: 5px 12px;
  font-size: 12px;
}
.closeButtonClass {
  display: flex;
  justify-content: center;
  align-content: center;
  border: none !important ;
}
.closeButtonClass .btn {
  background-color: rgba(228, 118, 8, 0.897);
  color: white;
  padding: 5px 12px;
  font-size: 12px;
}
.detailsSection {
  margin-bottom: 30px;
  margin-left: 50px;
}
</style>