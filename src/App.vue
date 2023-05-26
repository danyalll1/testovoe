<script setup>

import axios from 'axios'
import { ref,  onMounted} from 'vue'

let res = ref({})

const getData = () => {
  axios
  .get('https://test.tspb.su/test-task/vehicles')
  .then((response) => res = response.data)
      
  .catch((error) => console.log(error));
}





onMounted( () => {
  getData()
  })






</script>

<template>
  <header>
  
  </header>

  <body>
    <div class="container">
      <div class="cards__container" >
          <ul class="cards__card" v-for="item in res" key="item.id">
           <input type="text"  placeholder="color"> 
           {{ item.color }}
          </ul>
      </div>
   
    </div>
  </body>
</template>

<style scoped>

</style>
