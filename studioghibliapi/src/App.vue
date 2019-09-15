<template>
  <div>
    <h1>Anime List Yo</h1>
    <film-detail :film='selectedFilm'></film-detail>
    <films-list :films='films'></films-list>
  </div>
</template>

<script>
import ListComponent from './components/ListComponent.vue';
import FilmsList from './components/FilmsList.vue';
import FilmDetail from './components/FilmDetail.vue';
import {eventBus} from './main.js'
export default {
  name: 'app',
  data(){
    return {
      films: [],
      selectedFilm: null
    };
  },
  mounted(){
    fetch('https://ghibliapi.herokuapp.com/films')
    .then(res => res.json())
    .then(films => {
      films.forEach(film => {
        film.favourited = false
      })
      this.films = films
    })
    eventBus.$on('film-selected', (film) => {
      this.selectedFilm = film
    })
    eventBus.$on('film-favourited', (film) => {
      console.log("Howdy!")
      if (film.favourited === false) {
        film.favourited = true
      }
      else {
        film.favourited = false
      }
    })
  },

  components: {
    "films-list": FilmsList,
    "film-detail": FilmDetail
  }
}
</script>

<style>

</style>
