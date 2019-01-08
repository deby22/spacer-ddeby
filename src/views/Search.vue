<template>
    <div class="wrapper">
    <Claim />
    <SearchInput />
    </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';

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
      SearchInput,
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
    margin: 0;
    width: 100%;
    height: 100vh;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background-image: url('../assets/heroimage.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 80% 0%;
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
