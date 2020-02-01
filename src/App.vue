<template>
  <div :class="[{ flexStart: step ===1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg" alt="logo" class="logo" v-if="step === 1"></transition>
    
    <transition name="fade">
    <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    
    <div class="results" v-if="results && !loading && step === 1">

      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" />
    <!-- tak mozna sprawdzic co jest w danych 

    <div v-for="item in results" :key="item.data[0].nasa_id">

        <p>{{ item.links[0].href }}</p>

    </div> -->
    </div>
    <Modal />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
//import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov';

export default {
    name: 'App',
    components: { 
        HeroImage,
        Claim,
        SearchInput,
        Item
        //Modal
        },
    /* data w komponencie musi byc funkcja, która zwraca obiekt. 
     nie moze być czystym obiektem. */
    data() {
        return {
            /*Gdy deklarujemy v-model z jakas zmienną, musimy o pamietac o tym, ze ta zmienna musi miec jaka INICJALNA wartos w data */
            loading: false,
            step: 0,
            searchValue: '',
            results: [],
        };

    },
    methods: {
        handleInput: debounce (function(){
            this.loading = true;
            axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
                .then((response) =>{
                    this.results = response.data.collection.items;
                    this.loading = false;
                    this.step = 1;
                })
               
             
        }, 500),            
    },

};
</script>

<style> 
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,700&display=swap');
  
* {
  box-sizing: border-box;
}


body {
  font-family: 'Montserrat', sans-serif;
  margin: 0;
  padding: 0;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .3s ease;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top .3s ease;
}
.slide-enter, .slide-leave-to {
  margin-top: -50px;
}

.wrapper {
  margin: 0;
  position: relative;
  width: 100%;
  min-height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  /* &.flexStart {
    justify-content: flex-start ;
  } */
}
.logo {
  position:absolute;
  top: 30px;
}

.results {
  margin-top: 50px;
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  grid-gap: 20px;
}





</style>


