<script>
  export default {
    props: {
      setCrypto: {
        type: Function,
        required: true,
      },
      cryptoNow: {
        type: String,
        required: true,
      }
    }
  }
</script>

<template>
  <ul>
    <li @click="setCrypto('BTC')" :className="cryptoNow === 'BTC' ? 'active' : ''">Bitcoin</li>
    <li @click="setCrypto('ETH')" :className="cryptoNow === 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCrypto('USDT')" :className="cryptoNow === 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<style scoped>
  ul {
    list-style: none;
    width: 200px;
    padding: 0;
    border-radius: 3px;
    border: 3px solid #000;
  }

  li {
    display: block;
    background-color: #1a032d;
    color: white;
    padding: 20px 0;
  }

  li:hover {
    background-color: #24043e;
    cursor: pointer;
  }

  li.active {
    background-color: #0a0111;
  }
</style>
