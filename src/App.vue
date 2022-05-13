<template>
  <MainView
    v-if="mainView"
    :cryptos="filteredCryptos"
    :searchInputValue="searchInputValue"
    :mainView="mainView"
    @searchCryptos="searchInputValue = $event"
    :toggleViews="toggleViews"
    @activeCrypto="activeCrypto = $event"
  />
  <CryptoView v-else :toggleViews="toggleViews" :activeCrypto="activeCrypto" />
</template>

<script>
import MainView from './components/MainView.vue';
import CryptoView from './components/CryptoView.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    MainView,
    CryptoView,
  },

  data: () => ({
    cryptos: [],
    activeCrypto: {},
    mainView: true,
    dataLoading: true,
    searchInputValue: '',
  }),

  mounted() {
    axios
      .get('http://api.ampr.network/v1/coin/list_test')
      .then(({ data }) => {
        console.log(data);
        this.cryptos = data;
      })
      .finally((this.dataLoading = false));
  },

  methods: {
    toggleViews() {
      this.mainView = !this.mainView;
    },
  },

  computed: {
    filteredCryptos() {
      const newArr = this.cryptos.filter(
        ({ name }) =>
          name.indexOf(this.searchInputValue) > -1 ||
          name.toLowerCase().indexOf(this.searchInputValue) > -1
      );

      return newArr;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600&display=swap');

* {
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
  font-weight: 400;
}

body {
  margin: 0;
}
</style>
