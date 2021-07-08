<template>
  <div :class="[ {flexStart: step === 1},'wrapper' ]">
    <transition name="slide">
      <img src="../assets/logo.svg" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
      <Background v-if="step === 0"/>
    </transition>

    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1">
      <Item
        v-for="item in results"
        :item="item"
        :key="item.data[0].nasa_id"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loader" v-if="step === 1 && loading" />
    <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false" />
  </div>
</template>
<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
// eslint-disable-next-line import/extensions
import Claim from '@/components/Claim';
// eslint-disable-next-line import/extensions
import SearchInput from '@/components/SearchInput';
// eslint-disable-next-line import/extensions
import Background from '@/components/Background';
// eslint-disable-next-line import/extensions
import Item from '../components/Item';
import Modal from '../components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Modal, Item, Background, SearchInput, Claim,
  },
  data() {
    return {
      modalOpen: false,
      searchValue: '',
      results: [],
      loading: false,
      step: 0,
    };
  },
  methods: {
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },
    // eslint-disable-next-line max-len
    // debounce powoduje opuznienie wykonania zapytania dzieki czemu mamy czas na wpisanie calego zapytania
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          console.log(response.data.collection.items);
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

  .wrapper{
    width: 100%;
    height: 100vh;
    position: relative;
    margin: 0;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #fff;
    text-shadow: 0px 0px 10px rgba(255, 255, 255, 0.46);

    &.flexStart{
      justify-content: flex-start;
    }

    .results{
      margin-top: 50px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-gap: 20px;

      @media (min-width: 768px) {
        grid-template-columns: 1fr 1fr 1fr;
      }

      /*@media (min-width: 1400px) {*/
      /*  grid-template-columns: 1fr 1fr 1fr 1fr;*/
      /*}*/
    }
  }
  .logo {
    position: absolute;
    top: 30px;
  }

  .loader {
    margin-top: 100px;
    display: inline-block;
    width: 64px;
    height: 64px;
    @media (min-width: 768px) {
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
    @media (min-width: 768px) {
      width: 90px;
      height: 90px;
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
</style>
