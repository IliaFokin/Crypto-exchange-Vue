<script>
  import CryptoConvert from 'crypto-convert';
  import Input from './components/Input.vue';
  import Selector from './components/Selector.vue';
  import Favorite from './components/Favorite.vue';

  const convert = new CryptoConvert();

  export default {
    components: { Input, Selector, Favorite },
    data() {
      return {
        amount: 0,
        cryptoFirst: '',
        cryptoSecond: '',
        error: '',
        result: 0,
        favs: [],
      }
    },
    methods: {
      changeAmount(value) {
        this.amount = value;
      },
      setCryptoFirst(value) {
        this.cryptoFirst = value;
      },
      setCryptoSecond(value) {
        this.cryptoSecond = value;
      },
      async convert() {
        if (this.amount <=0) {
          this.error = 'Введите число больше 0';
          return;
        } else if (this.cryptoFirst === '' || this.cryptoSecond === '') {
          this.error = 'Выберите валюту';
          return;
        } else if (this.cryptoFirst === this.cryptoSecond) {
          this.error = 'Выберите другую валюту';
          return;
        }
        this.error = '';

        await convert.ready();

        if (this.cryptoFirst === 'BTC' && this.cryptoSecond === 'ETH')
          this.result = convert.BTC.ETH(this.amount);
        else if (this.cryptoFirst === 'BTC' && this.cryptoSecond === 'USDT')
          this.result = convert.BTC.USDT(this.amount);
        else if (this.cryptoFirst === 'ETH' && this.cryptoSecond === 'BTC')
          this.result = convert.ETH.BTC(this.amount);
        else if (this.cryptoFirst === 'ETH' && this.cryptoSecond === 'USDT')
          this.result = convert.ETH.USDT(this.amount);
        else if (this.cryptoFirst === 'USDT' && this.cryptoSecond === 'BTC')
          this.result = convert.USDT.BTC(this.amount);
        else if (this.cryptoFirst === 'USDT' && this.cryptoSecond === 'ETH')
          this.result = convert.USDT.ETH(this.amount);
      },
      favorite () {
        if (this.cryptoFirst !== '' && this.cryptoSecond !== '') {
          this.favs.push({
            from: this.cryptoFirst,
            to: this.cryptoSecond,
          })
        }
      },
      getFromFavs(index) {
        this.cryptoFirst = this.favs[index].from;
        this.cryptoSecond = this.favs[index].to;
      }
    }
  }
</script>

<template>
  <h1>CRYPTO</h1>
  <Input 
    :changeAmount="changeAmount"
    :convert="convert"
    :favorite="favorite"
  />
  <p v-if="error !== ''">{{ error }}</p>
  <p v-if="result !== 0" className="result-text">{{ result }}</p>
  <Favorite
    v-if="favs.length > 0"
    :favs="favs"
    :getFromFavs="getFromFavs"
  />
  <div className="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst"/>
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond"/>
  </div>
</template>

<style scoped>
  .selectors {
    display: flex;
    justify-content: space-around;
    margin-top: 30px;
    width: 700px;
  }

  .result-text {
    font-family: 'Nabla', cursive;
    font-size: 2em;
  }
</style>
