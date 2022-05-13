<template>
  <button class="crypto-view__exit" @click="toggleViews">
    <img src="../assets/cross.svg" alt="close" />
  </button>
  <h1 class="crypto-view__heading">Receive {{ activeCrypto.symbol }}</h1>
  <div class="crypto-view__container">
    <div class="crypto-view__icon-container">
      <img
        class="crypto-view__icon-icon"
        :src="activeCrypto.icon"
        :alt="activeCrypto.name"
      />
    </div>
  </div>
  <div class="crypto-view__blue-container">
    <h4>0,043143 {{ activeCrypto.symbol }}</h4>
    <h6>€100,00</h6>
  </div>
  <div class="crypto-view__qr-container">
    <vue-qrcode :value="activeCrypto.wallet" :width="150" />
  </div>
  <div class="crypto-view__wallet">
    <h3 class="crypto-view__subheading">wallet address</h3>
    <div class="crypto-view__wallet-container">
      {{ activeCrypto.wallet.slice(0, 12) }}...{{
        activeCrypto.wallet.substr(activeCrypto.wallet.length - 12)
      }}
      <button class="crypto-view__wallet-copy" @click="copyWalletCode">
        <img src="../assets/copy.svg" alt="copy" />
      </button>
    </div>
    <div class="crypto-view__warning">
      send only usdt to this deposit address ensure the network is
      <span class="crypto-view__warning--red">ethereum (erc20)</span>
    </div>
    <div class="crypto-view__buttons">
      <button @click="copyWalletCode" class="crypto-view__copy-button">
        Copy Address
      </button>
      <button class="crypto-view__share-button">Share Address</button>
    </div>
  </div>
</template>

<script>
import VueQrcode from 'vue-qrcode';
export default {
  components: {
    VueQrcode,
  },
  name: 'CryptoView',
  data: () => ({
    walletCode: '',
  }),
  props: {
    activeCrypto: Object,
    toggleViews: Function,
  },
  emits: ['searchCryptos'],
  methods: {
    copyWalletCode() {
      this.walletCode = this.activeCrypto.walletCode;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.crypto-view__exit {
  border: none;
  background-color: transparent;
  position: absolute;
  right: 10px;
  top: 10px;
}

.crypto-view__heading {
  margin-top: 20px;
  font-size: 24px;
  margin-bottom: 0;
}

.crypto-view__container {
  display: flex;
  justify-content: center;
  position: relative;
}

.crypto-view__icon-container {
  padding: 10px 15px 10px;
  background-color: white;
  border-radius: 50px;
  position: relative;
  z-index: 3;
}

.crypto-view__icon-icon {
  width: 50px;
  height: 50px;
}

.crypto-view__blue-container {
  padding: 5px;
  width: 100%;
  height: 160px;
  background-color: rgba(118, 120, 242, 0.15);
  position: relative;
  margin-top: -10px;
  z-index: 2;
  border-radius: 20px 20px 0 0;
}

.crypto-view__qr-container {
  width: 160px;
  height: 160px;
  border: solid 5px rgba(118, 120, 242, 0.25);
  background-color: white;
  border-radius: 10px;
  margin: 0 auto;
  position: relative;
  margin-top: -80px;
  margin-bottom: 10px;
  z-index: 3;
}

.crypto-view__subheading {
  text-align: center;
  text-transform: uppercase;
  font-size: 10px;
}

.crypto-view__wallet {
  width: 100%;
  padding: 0 15px;
}

.crypto-view__wallet-container {
  background-color: rgba(118, 120, 242, 0.15);
  padding: 5px 30px 5px 10px;
  width: 100%;
  text-align: center;
  position: relative;
}

.crypto-view__wallet-copy {
  position: absolute;
  right: 3px;
  top: 3px;
  width: 30px;
  height: 30px;
  border: none;
  background-color: transparent;
}

.crypto-view__warning {
  margin: 10px 0 30px;
  text-align: center;
  font-size: 10px;
  text-transform: uppercase;
}

.crypto-view__warning--red {
  color: red;
}

.crypto-view__buttons {
  display: flex;
  flex-direction: column;
}

.crypto-view__copy-button,
.crypto-view__share-button {
  font-weight: 600;
  outline: none;
  margin-bottom: 10px;
  border-radius: 4px;
  padding: 8px;
  border: 2px rgba(22, 22, 249, 0.7) solid;
}

.crypto-view__copy-button {
  color: rgba(22, 22, 249, 0.7);
  background-color: transparent;
}

.crypto-view__share-button {
  color: white;
  background-color: rgba(22, 22, 249, 0.7);
}

h1,
h4,
h6 {
  text-align: center;
}

h1,
h4 {
  font-weight: 600;
}

h4,
h6 {
  line-height: 0;
}
</style>
