<template>
  <div>
    <h1 class="main-view__heading">Receive</h1>
    <h4 class="main-view__subheading">choose a wallet to recieve crypto to</h4>
    <div class="main-view__search-container">
      <label>
        <input
          class="main-view__search-input"
          type="text"
          :value="searchInputValue"
          @input="$emit('searchCryptos', $event.target.value)"
        />
        <img
          class="main-view__search-icon"
          src="../assets/loupe.svg"
          alt="search"
        />
      </label>
    </div>
    <div class="main-view__cryptos">
      <div
        class="main-view__crypto"
        v-for="crypto in cryptos"
        :key="crypto.id"
        @click="getCryptoInfo(crypto)"
      >
        <div class="main-view__crypto-info">
          <img
            :src="crypto.icon"
            :alt="crypto.name"
            class="main-view__crypto-icon"
          />
          <div>
            <h2>{{ crypto.name }}</h2>
            <h4>{{ crypto.symbol }}</h4>
          </div>
        </div>
        <div class="main-view__crypto-wallet">
          <h3>0,0 {{ crypto.symbol }}</h3>
          <h5>€0,00</h5>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainView',
  props: {
    cryptos: Array,
    searchInputValue: String,
    toggleViews: Function,
    activeCrypto: Object,
  },
  emits: ['searchCryptos', 'activeCrypto'],
  methods: {
    getCryptoInfo(info) {
      this.$emit('activeCrypto', info);
      this.toggleViews();
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main-view__heading {
  font-weight: 600;
  font-size: 24px;
  text-align: center;
}

.main-view__subheading {
  text-align: center;
  text-transform: uppercase;
  font-size: 12px;
}

.main-view__search-container {
  width: 100%;
  padding: 0 25px;
  margin-bottom: 20px;
}

.main-view__search-input {
  width: 100%;
  padding: 5px 10px;
  background-color: rgba(118, 120, 242, 0.15);
  border: none;
  outline: none;
  border-radius: 4px;
}

.main-view__search-icon {
  position: absolute;
  right: 10px;
  top: 5px;
}

label {
  position: relative;
}

.main-view__cryptos {
  border: 4px solid rgba(118, 120, 242, 0.15);
  border-radius: 8px;
  border-collapse: collapse;
  width: 100%;
  height: 500px;
  overflow: scroll;
}

.main-view__crypto {
  display: flex;
  justify-content: space-between;
}

.main-view__crypto {
  padding: 0 15px;
  border-bottom: 2px solid rgba(118, 120, 242, 0.15);
  border-top: 2px solid rgba(118, 120, 242, 0.15);
  border-radius: 8px;
}

.main-view__crypto:last-child {
  border-bottom: none;
}

.main-view__crypto:first-child {
  border-top: none;
}

.main-view__crypto-info {
  display: flex;
  align-items: center;
}

.main-view__crypto-icon {
  width: 50px;
  height: 50px;
  margin-right: 15px;
}

h2,
h3 {
  font-weight: 600;
}

h2 {
  line-height: 20px;
}

h3 {
  line-height: 16px;
}

h4,
h5 {
  line-height: 10px;
}

.main-view__crypto-wallet {
  text-align: end;
}
</style>
