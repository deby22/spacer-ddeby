<template>
    <div class="wrapper">
    <Claim />
        <div class="search">
            <label for="search">Search</label>
            <input @input="handleInput" id="search" name="search" v-model="searchValue" />
        </div>
    </div>
</template>

<script>

import Claim from '@/components/Claim.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  components: {
    Claim,
  },
  methods: {

    // eslint-disable-next-line
    handleInput: debounce(function(){
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>


<style lang="scss" scoped>
.wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
}

.search {
    display: none;
    flex-direction: column;
    width: 300px;

    label {
        font-family: Montserat, sans-serif;
    }

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
    }
}
</style>
