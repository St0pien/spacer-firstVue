<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
      <img src="./assets/logo.svg" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
      <HeroImage v-if="step ===  0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="results" v-if="results && !loading && step === 1">
      <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id"
      @click.native="handleModalOpen(item)" />
    </div>
    <div class="loader" v-if="step === 1 && loading" />
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen=false" />
  </div>
</template>

<script>
/* eslint-disable */ 
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',
  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },
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
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

    // eslint-disable-next-line
    handleInput: debounce(function () {
      this.loading = true;
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

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  body {
    font-family: "Montserrat", sans-serif;
    margin: 0;
    padding: 0;
    background: linear-gradient(white, #333);
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .5s ease;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top .5s ease;
  }

  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

  .wrapper {
    width: 100%;
    position: relative;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 30px;

      &.flexStart {
      justify-content: flex-start;
    }
  }

  .loader {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, );
    display: inline-block;
    width: 64px;
    height: 64px;
  }

  .loader::after {
    content: '';
    display: block;
    width: 46px;
    height: 46px;
    margin: 1px;
    border-radius: 50%;
    border: 5px solid #1e3d4a;
    border-color: #1e3d4a transparent #1e3d4a transparent;
    animation: loading 1.2s linear infinite;

    @media (min-width: 768px) {
      width: 90px;
      height: 90px
    }
  }

  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }

    100% {
      transform: rotate(360deg);
    }
  }

  .logo {
    position: absolute;
    top: 30px;
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
