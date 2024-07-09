<script>
  export default {
    props: {
      changeAmount: {
        type: Function,
        required: true,
      },
      convert: {
        type: Function,
        required: true,
      },
      favorite: {
        type: Function,
        required: true,
      }
    }
  }
</script>

<template>
  <input min="0" type="number" @input="changeAmount($event.target.value)" placeholder="Введите число">
  <br>
  <button @click="convert()">Конвертировать</button>
  <button @click="favorite()" className="fav-button">В избранное</button>
</template>

<style scoped>
  input {
    margin-top: 20px;
    padding: 10px 15px;
    width: 500px;
    border: 0;
    border-radius: 3px;
    outline: none;
    color: #333;
    background-color: #fafafa;
    font-size: 1.2em;
  }

  button {
    margin-top: 20px;
    padding: 15px 20px;
    color:  white;
    text-transform: uppercase;
    cursor: pointer;
    background-color: #1a032d;
    border: 0;
    border-radius: 3px;
  }

  .fav-button {
    margin-left: 20px;
  }
</style>
