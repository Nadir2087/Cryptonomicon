<template>
      <section>
      <div class="flex">
        <div class="max-w-xs">
          <label for="wallet" class="block text-sm font-medium text-gray-700"
            >Тикер</label
          >
          <div class="mt-1 relative rounded-md shadow-md">
            <input
              v-model="name_coin"
              type="text"
              name="wallet"
              id="wallet"
              class="block w-full pr-10 border-gray-300 text-gray-900 focus:outline-none focus:ring-gray-500 focus:border-gray-500 sm:text-sm rounded-md"
              placeholder="Например DOGE"
              @keypress.enter="addCoin"
            />
          </div>
          <div class="flex bg-white shadow-md p-1 rounded-md shadow-md flex-wrap">
            <span @click="clickOn('BTC')" class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer">
              BTC
            </span>
            <span @click="clickOn('DOGE')" class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer">
              DOGE
            </span>
            <span @click="clickOn('BCH')" class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer">
              BCH
            </span>
            <span @click="clickOn('CHD')" class="inline-flex items-center px-2 m-1 rounded-md text-xs font-medium bg-gray-300 text-gray-800 cursor-pointer">
              CHD
            </span>
          </div>
          <div class="text-sm text-red-600">{{error}}</div>
        </div>
      </div>
      <button @click="addCoin"
        type="button"
        class="my-4 inline-flex items-center py-2 px-4 border border-transparent shadow-sm text-sm leading-4 font-medium rounded-full text-white bg-gray-600 hover:bg-gray-700 transition-colors duration-300 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-gray-500"
      >
        <!-- Heroicon name: solid/mail -->
        <svg
          class="-ml-0.5 mr-2 h-6 w-6"
          xmlns="http://www.w3.org/2000/svg"
          width="30"
          height="30"
          viewBox="0 0 24 24"
          fill="#ffffff"
        >
          <path
            d="M13 7h-2v4H7v2h4v4h2v-4h4v-2h-4V7zm-1-5C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm0 18c-4.41 0-8-3.59-8-8s3.59-8 8-8 8 3.59 8 8-3.59 8-8 8z"
          ></path>
        </svg>
        Добавить
      </button>
    </section>
</template>

<script>
import axios from 'axios'
export default {
    name: 'c-add-coin',
    data(){
        return{
            name_coin: '',
            info_coin: [],
            error: ''
        }
    },
    methods:{
        async addCoin(){
            if(this.name_coin == ''){
                this.error = 'Напишите название криптоволюты!'
                this.name_coin = ''

            }else{
                const api = await axios.get('https://min-api.cryptocompare.com/data/pricemulti?fsyms='+ this.name_coin +'&tsyms=USD&api_key=9f936104af548f59ac7ae1e52d6a42c2a2ba478b2a256ba0712c05b0810c4e25')
                this.info_coin = api.data
                if(typeof this.info_coin['Response'] !== "undefined"){
                    this.error = 'Такого коина у нас нету!'
                    this.name_coin = ''
                }else{
                    this.$emit('addCoin', this.info_coin, this.name_coin)
                    this.error = ''
                    this.name_coin = ''
                }
                // if(api.data.length === 7){
                //     this.info_coin = ''
                // }else{

                // }

            }
            
        },
        clickOn(data){
            this.name_coin = ''
            this.name_coin = data
        }
    }

}
</script>

<style>

</style>