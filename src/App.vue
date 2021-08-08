<template>
  <img v-bind:alt="imageAlt" :src="imageSrc">

  <div>
    <div>{{ title }} </div>

    <ul>
      <li v-for="(item, index) of items" :key="item" @click="onListItemClick(item)">
        {{item}} - {{index}}
      <button @click="itemRemove(item, index)"> remove </button>
      </li>
    </ul>

    <h1 v-if="counter === 0"> Hello</h1>
    <h1 v-else> World </h1>

    <Counter :counter="counter" @handleIncClick="incHandler" @handleDecClick="decHandler"/>
  </div>
</template>

<script>

import Counter from "./components/Counter";
import Img from './assets/logo.png'

export default {
  name: 'App',
  components: {
    Counter
  },
  data() {
    return {
      counter: 0,
      title: 'Dynamic Text',
      imageAlt: 'Vue logo',
      imageSrc: Img,
      items: [1, 2, 3, 4]
    }
  },
  methods: {
    onListItemClick(itemVal) {
      console.log(itemVal)
    },
    incHandler() {
      this.counter++;
    },

    decHandler() {
      this.counter--;
    },

    itemRemove(item) {
      this.items = this.items.filter(el => el !== item)
    }

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
