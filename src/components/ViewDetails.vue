<template>

    <div class="border border-primary detailsContent">
     <p class="text-center p-0 m-0">
     ViewDetails
     </p>
     
     <div class="text-center p-0 m-0 mb-3">
     ………………………………………………
     </div>
     <div>
     <div>
     Name : {{props.selectedProduct?.title}}
    </div>
     <div>
     Price : {{props.selectedProduct?.price}}
    </div>
     <div>
     Rating : {{props.selectedProduct?.rating}}
    </div>
     <div>
     Description : {{props.selectedProduct?.description}}
    </div>
     </div>
     </div>
</template>

<script setup>
   const props = defineProps(['selectedProduct'])
   console.log("selectedProduct", props.selectedProduct);
</script>

<style scoped>
.detailsContent{
   border-radius: 30px;
  width: 100%;
 padding: 40px 15px;
 margin-bottom: 50px;
 margin-top: 20px;

}
</style>