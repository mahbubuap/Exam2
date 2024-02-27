<script setup>
import ListUpdate from './components/ListUpdate.vue';
import  FormUpdate  from  './components/FormUpdate.vue'
</script>

<template>

  <div  class="mb-10">
   <ListUpdate/>
  </div>

  <div> 
  <FormUpdate/>
  
  </div>

 

</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
