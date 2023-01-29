<template>
  <div class="App">
    <div class="container mx-auto flex flex-col items-center bg-gray-100 p-4">
      <div class="container">
        <cAddCoin @addCoin = 'addCoin' />
        <hr v-if="names_coin.length" class="w-full border-t border-gray-600 my-4" />
        
        <div class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">  
          <cCardCoin v-for="(card,inx) in names_coin" :key="inx" :name_card="card" :name_space="names_space[inx]" @activeCoin="activeCoin"/>
          <!-- <cCardCoin/>
          <cCardCoin/>
          <cCardCoin class="border-4 "/>
          <cCardCoin class=""/> -->
        </div>
        <div v-if="active">
        <hr class="w-full border-t border-gray-600 my-4" />
          <cInfoCoin/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import cAddCoin from './components/c-add-coin.vue';
import cCardCoin from './components/c-card-coin.vue'
import cInfoCoin from './components/c-info-coin.vue'

export default {
  name: 'App',
  data(){
    return{
      names_space: [],
      names_coin: [],
      active: false
    }
  },
  components: {
    cAddCoin,
    cCardCoin,
    cInfoCoin
  },
  methods:{
    addCoin(data, name){
      this.names_space.push(name)
      this.names_coin.push(data)
    },
    activeCoin(data){
      this.active=data
    }
  },
  mounted(){

  }
}
</script>

<style>
@import './styles/app.css';
</style>
