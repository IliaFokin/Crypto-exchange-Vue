<script>
  export default {
    props: {
      favs: {
        type: Array,
        required: true,
      },
      getFromFavs: {
        type: Function,
        required: true,
      }
    }
  }
</script>

<template>
  <h2>Варианты в избранном</h2>
  <div v-for="(el, index) in favs" @click="getFromFavs(index)" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<style scoped>
  h2 {
    margin-top: 30px;
    color: white;
  }

  div {
    display: flex;
    justify-content: space-between;
    margin: 10px auto;
    width: 500px;
    transition: all .5s ease-in-out;
  }

  div:hover {
    opacity: 0.7;
    transform: scale(1.1);
    cursor: pointer;
  }

  span {
    padding: 10px 15px;
    background-color: #8c00ff;
    color: white;
  }
</style>
