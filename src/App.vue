<template>
    <div :class="[{ flexStart: step === 1 }, 'wrapper']">
        <transition name="slide">
            <img src="./assets/logo.png" class="logo" v-if="step === 1">
        </transition>
        <transition name="fade">
            <HeroImage v-if="step === 0"/>
        </transition>
        <Claim v-if="step === 0" />
        <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
        <div class="results" v-if="results && !loading && step === 1">
            <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModalOpen(item)"/>
        </div>
        <div class="loader" v-if="step === 1 && loading" />
        <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
    </div>
</template>

<script>

import Claim from '@/components/Claim.vue';
import HeroImage from '@/components/HeroImage.vue';
import SearchInput from '@/components/SearchInput.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search';

export default {
    name: 'App',
    data() {
        return {
            modalOpen: false,
            modalItem: null,
            loading: false,
            step: 0,
            searchValue: '',
            results: [],
        };
    },
    components: {
        Claim,
        SearchInput,
        HeroImage,
        Item,
        Modal,
    },
    methods: {
        handleModalOpen(item){
            this.modalOpen = true;
            this.modalItem = item;
        },

        // eslint-disable-next-line
        handleInput: debounce(function(){
            this.loading = true;
            console.log(this.searchValue);
            axios.get(`${API}?q=${this.searchValue}&media_type=image`)
                .then((response) => {
                    this.results = response.data.collection.items;
                    this.loading = false;
                    this.step = 1;
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
    position: relative;
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
    font-family: 'Montserrat', sans-serif;
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

body {
    margin: 0;
    padding: 0;
}

.flexStart {
    justify-content: flex-start;
}

.slide-enter-active, .slide-leave-active {
    transition: margin-top .3s ease;
}
.slide-enter, .slide-leave-to{
    margin-top: -100px;
}

.fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
}
.fade-enter, .fade-leave-to{
    opacity: 0;
}



.logo {
    position: absolute;
    top: 40px;
}


.results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media(min-width: 768px){
        grid-template-columns: 1fr 1fr 1fr;
    }

}

.loader {
    margin-top: 100px;
    display: inline-block;
    width: 64px;
    height: 64px;

    @media(min-width: 768px){
        width: 90px;
        height: 90px;
    }
}
.loader:after {
    content: " ";
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;
}
@keyframes loading {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}



</style>
