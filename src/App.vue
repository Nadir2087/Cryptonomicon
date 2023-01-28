<template>
  <div class="App">
    <div class="container mx-auto flex flex-col items-center bg-gray-100 p-4">
      <div class="container">
        <cAddCoin/>
        <hr class="w-full border-t border-gray-600 my-4" />
        <div class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
          <cCardCoin/>
          <cCardCoin/>
          <cCardCoin/>
          <cCardCoin class="border-4 "/>
          <cCardCoin class=""/>
        </div>
        <hr class="w-full border-t border-gray-600 my-4" />
        <cInfoCoin/>
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
  components: {
    cAddCoin,
    cCardCoin,
    cInfoCoin
  }
}
</script>

<style>
@import './styles/app.css';
</style>
