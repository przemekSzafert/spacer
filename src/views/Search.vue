<template>
    <div class="wrapper">
    <div class="search">
        <label for="search">Search</label>
        <input 
            id="search" 
            name="search"
            v-model="searchValue"
            @input="handleInput"
        />
        <ul>
            <li v-for="item in results" :key="item.data[0].nasa_id">
                <p>{{ item.data[0].description }}</p>
            </li>
        </ul>
    </div>
    </div>
</template>



<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
const API = 'https://images-api.nasa.gov';

export default {
    name: 'Search',
    /* data w komponencie musi byc funkcja, która zwraca obiekt. 
     nie moze być czystym obiektem. */
    data() {
        return {
            /*Gdy deklarujemy v-model z jakas zmienną, musimy o pamietac o tym, ze ta zmienna musi miec jaka INICJALNA wartos w data */
            searchValue: '',
            results: [],
        };

    },
    methods: {
        handleInput: debounce (function(){
            axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
                .then((response) =>{
                    this.results = response.data.collection.items;
                })
               
             
        }, 500),            
    },

};
</script>
//lang="scss" scoped
<style >

    .wrapper {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 0;
        padding: 30px;
        width: 100%;
    }

    .search {
        display: flex;
        flex-direction: column;
        width: 250px;
    }

    label {
        font-family: monospace,sans-serif;
    }

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
    }

</style>