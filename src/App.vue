<template>
    <div class="wrapper">
    <HeroImage />
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput"/>
    </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import HeroImage from '@/components/HeroImage.vue';
import SearchInput from '@/components/SearchInput.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  components: {
      Claim,
      SearchInput,
      HeroImage,
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
    min-height: 100vh;
    height: 100vh;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}

.search {
    display: none;
    flex-direction: column;
    width: 300px;

    label {
        font-family: Montserrat, sans-serif;
    }

    input {
        height: 30px;
        border: 0;
        border-bottom: 1px solid black;
    }
}

@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

$font-weight-light: 300;
$font-weight-normal: 400;
$font-weight-bold: 600;
$font-weight-black: 800;

*{
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

body {
    font-family: 'Montserrat', sans-serif;
    margin: 0;
    padding: 0;
}
</style>
