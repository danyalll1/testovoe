<script setup>

import axios from 'axios'
import { ref,  onMounted, computed} from 'vue'

async function getData() {
  try{
    await axios.get(link)
    .then((response) => {
    res.value = response.data
    isLoading = true
    
   })
  }
  catch(error) {
    console.log(error)
  }
}



let res = ref()
let  link = 'https://test.tspb.su/test-task/vehicles'
let isLoading = false
const query = ref('year')

const sortRes = computed(() => {
    if (query.value === 'year')
    return res.value.sort((a,b)=>a.year > b.year ? -1 : 1)
    if (query.value = 'price')
    return res.value.sort((a,b)=>a.price > b.price ? -1 : 1)
})

  
onMounted( () => {
  getData()
  })


 



</script>

<template>
  <header>
  
  </header>

  <body>
    <div class="container">
      <div class="filter-container">
        <select class="filter-container__filter" v-model="query" name="Filter" id="1">
          <option class="selector" value="year">Год выпуска</option>
          <option class="selector" value="price">Цена</option>
        </select>
      </div>
        <div class="cards-container" v-for="(item,n) in res" :key="n">
          <div v-if="isLoading">
              <div class="contacardsiner__card">
                Марка:<input class="inputs" type="input" v-model="res[n].name">
                Модель:<input class="inputs" type="input" v-model="res[n].model">
                Цена:<input class="inputs" type="input" v-model="res[n].price">
                <div class="card__info">
                  <div style="display: flex;">
                    <span class="text">Цвет:</span>
                    <div class="color"  :style="{ backgroundColor: item.color}" ></div>
                  </div>
                  
                  <span class="text">{{ item.year }}</span>
                </div>
                
              </div>
          </div>
        
        </div>
      </div>
    
  </body>
</template>

<style scoped>
.container{
  font-weight: 700;
  font-family: 'IBM Plex Sans', sans-serif;
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
}

.inputs{
  background-color: (255,255,255);
  border: none;
  border-radius: 16px;
}

.contacardsiner__card{
  justify-content: space-between;
  color: rgb(61, 54, 94);
  box-shadow: 1px 4px 7px rgba(96, 104, 101, 0.3);
  border: solid rgba(7, 11, 228, 0.342);
  border-radius: 22px;
  background-color: rgba(255, 255, 255, 0.3);
  width: 250px;
  height: auto;
  padding: 22px;
  margin: 0 20px 20px 0;
  display: flex;
  flex-direction: column;
}
.inputs{
  padding-left: 15px;
  height: 30px;
  font-family: 'IBM Plex Sans', sans-serif;
  font-style: italic;
  background-color: rgba(47, 31, 133, 0.2);
  margin-bottom: 15px;
  outline: none;
}

.card__info{
  display: flex;
  justify-content: space-between;
}

.text{
  color: rgb(54, 94, 78);
  display: block;
}
.color{
  height: 15px;
  width: 15px;
  margin-top: 3px;
  margin-left: 10px;
}

.filter-container{
  position: absolute;
  left: 10px;
}

.filter-container__filter{
  width: 100px;
  height: 30px;
  outline: none;
  border-radius: 16px;
  margin-left: 15px;
  margin-top: 2px;
  cursor: pointer;
}

</style>
