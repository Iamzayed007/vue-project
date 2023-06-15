<template>
    <tbody v-for="(d,index) in dataPaginated" :key="d.id"> 
  <tr  class="border border-dark">
      <th scope="row" class="border border-dark">{{index+1}}</th>
      <td class="border border-dark">{{d.title}}</td>
      <td class="border border-dark">{{d.rating}}</td>
      <td class="border border-dark">{{d.price}}</td>
      <td v-if="selectedUserId != d.id" class="border border-dark buttonClass">
      <button   class="btn text-sm-center" @click="toggleDetails(d.id)">
        Show
      </button>
      </td>
      <td v-if="selectedUserId == d.id" class="border border-dark closeButtonClass">
      <button   class="btn text-sm-center" @click="hideDetails">
        Close
      </button>
      </td>
    </tr>
 <tr  v-if="selectedUserId == d.id" class="detailsSection" >
   <ViewDetails :selectedUser="selectedUser" />
   </tr>
   </tbody>
    
</template>

<script setup>
import { ref, defineProps, defineEmits, provide } from 'vue';
 import ViewDetails from './ViewDetails.vue'
 import axios from 'axios';
const props = defineProps(
    [  "data","dataPaginated"]
)
const selectedUserId = ref(null);
const selectedUser = ref(null);


function toggleDetails(userId) {
  if (selectedUserId === userId) {
    hideDetails();
  } else {
    selectedUserId.value = userId;
    fetchUserDetails(userId);
  }
}

const fetchUserDetails = async(userId)=> {
      try {
    const response = await axios.get(`https://dummyjson.com/products/${userId}`);
    selectedUser.value  = response.data;
   
    console.log("selectedUser.value",selectedUser.value)
  } catch (error) {
    console.error('Error fetching data:', error);
  }
}

function hideDetails() {
  selectedUserId.value = null;
  selectedUser.value = null;
}

</script>

<style scoped>
.buttonClass{
    display: flex;
    justify-content: center;
    border: none !important ;
}
.buttonClass .btn{
    background-color: rgb(83, 157, 46);
    color: white;
    padding: 3px 5px;
    /* font-size: 1px; */
}
.closeButtonClass{
    display: flex;
    justify-content: center;
    border: none !important ;
}
.closeButtonClass .btn{
    background-color: rgb(217, 120, 24);
    color: white;
    padding: 3px 5px;
    /* font-size: 1px; */
}
.detailsSection{
    display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  margin-top: 10px ;
  margin-bottom: 30px;
  margin-left: 50px;
}
</style>