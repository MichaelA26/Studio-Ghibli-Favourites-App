<template lang="html">
  <div>
    <li
    v-bind:class="{'favourited' : film.favourited, 'notFavourited': !film.favourited}"
    v-on:click="handleClick">{{film.title}}
  </li>
  <button v-on:click="handleFavouriteClick">Add/Remove from Favourites</button>
</div>
</template>

<script>
import { eventBus } from '../main.js'
export default {
  name: 'list-component',
  props: ['film'],
  methods: {
    handleClick(){
      eventBus.$emit('film-selected', this.film)
    },
    handleFavouriteClick(){
      eventBus.$emit('film-favourited', this.film)
    }
  }
}
</script>

<style lang="css" scoped>
.favourited {
  color: green;
}
.notFavourited {
  color: red;
}
</style>
