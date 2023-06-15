<template>

    <div class="border border-primary detailsContent">
     <p class="text-center p-0 m-0">
     ViewDetails
     </p>
     
     <div class="text-center p-0 m-0">
     ………………………………………………
     </div>
     <div>
     <div>
     Name : {{props.selectedUser?.title}}
    </div>
     <div>
     Price : {{props.selectedUser?.price}}
    </div>
     <div>
     Rating : {{props.selectedUser?.rating}}
    </div>
     <div>
     Description : {{props.selectedUser?.description}}
    </div>
     </div>
     </div>
</template>

<script setup>
   const props = defineProps(['selectedUser'])
   console.log("selectedUser", props.selectedUser);
</script>

<style scoped>
.detailsContent{
   border-radius: 30px;
  width: 100%;
  padding: 20px 10px ;

}
</style>