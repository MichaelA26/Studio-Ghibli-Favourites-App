<template lang="html">
  <form v-on:submit.prevent>
    <input type="text" v-model="search" placeholder="Search for Film!" v-on:keyup="searchForFilm">
    <select v-on:change="handleSelect" v-model="selectedFilm">
      <option disabled value="">Select a film...</option>
      <option v-for="film in films" :value="film">{{film.title}}</option>
    </select>
  </form>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "film-filter-form",
  data(){
    return {
      "search": "",
      "selectedFilm": {},
    }
  },
  props: ["films"],
  methods: {
    searchForFilm(){
      let foundFilm = this.films.find((film) => {
        return film.title.toLowerCase().indexOf(this.search.toLowerCase()) > -1
      })
      this.selectedFilm = foundFilm
      eventBus.$emit('film-selected', this.selectedFilm)
    },
    handleSelect(){
      this.search = ""
      eventBus.$emit('film-selected', this.selectedFilm)
    }
  }
}
</script>

<style lang="css" scoped>
form{
  text-align: center;
  margin: 40px 0;
}
select, input[type="text"]{
  font-size: 18px;
}
select {
  margin-left: 20px;
}
</style>
