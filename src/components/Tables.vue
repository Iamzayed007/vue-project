<template>
 <Filter :sortBy="sortBy" :sortDirection="sortDirection" :sortData="sortData"  />
   <table class=" table table-light border border-dark">
  <thead>
    <tr>
      <th scope="col" class="border border-dark fw-bold">SI</th>
      <th scope="col" class="border border-dark fw-bold">Name</th>
      <th scope="col" class="border border-dark fw-bold">Rating</th>
      <th scope="col" class="border border-dark fw-bold">Price</th>
      <th scope="col" class="border border-dark fw-bold">Action</th>
    </tr>
  </thead>

<TableList   @update:handleShowDetails="handleShowDetails"
:data="data"
:dataPaginated="dataPaginated"
 />
</table>
<div  v-if="loading == false">

  <Pagination :count="data.products.length / 5" @current-page="setCurrentPage" :activePage="currentPage" />
</div>
</template>

<script setup>
 import { ref, onMounted ,computed} from 'vue'
import TableList from './TableList.vue'

 import Pagination from "./Pagination.vue";
 import Filter from "./Filter.vue";
import axios from 'axios';

const data = ref([]);
const loading = ref(true);

const currentPage = ref(1);
const itemsPerPage = 5;
 const sortBy = ref('');
const sortDirection = ref('');



const setCurrentPage = (index) => {
  console.log("SetCurrentPage", index);
  currentPage.value = index;
};
 // Fetch data from API
const fetchData = async () => {
  try {
    const response = await axios.get('https://dummyjson.com/products?limit=100');
    data.value = response.data;
    loading.value = false;
    console.log("data prob",data.value)
  } catch (error) {
    console.error('Error fetching data:', error);
  }
};

// Fetch data when component is mounted
onMounted(fetchData);

const sortData =(by,direction)=>{
     sortBy.value = by;
  sortDirection.value = direction;
}
const dataPaginated = computed(() => {
 
 const startIndex = (currentPage.value - 1) * itemsPerPage;
const endIndex = startIndex + itemsPerPage;
  if (sortBy.value || sortDirection.value) {
const sortedProducts =  data.value.products?.sort((a, b) => {
  const aValue = a[sortBy.value];
  const bValue = b[sortBy.value];

  if (aValue < bValue) {
    return sortDirection.value === 'asc' ? -1 : 1;
  }

  if (aValue > bValue) {
    return sortDirection.value === 'asc' ? 1 : -1;
  }

  return 0;
})


return sortedProducts.slice(startIndex, endIndex);}
 return data.value.products?.slice(startIndex, endIndex);
});
</script>

<style >

</style>