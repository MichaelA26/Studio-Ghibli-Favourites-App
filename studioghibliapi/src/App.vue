<template>
  <div>
    <h1>Studio Ghibli Film List</h1>
    <film-filter-form :films='films'></film-filter-form>
    <p>Select your favourite films by clicking on the add/remove button!</p>
    <p>Green text = Favourited and Red Text = Not Favourited</p>
    <film-detail :film='selectedFilm'></film-detail>
    <films-list :films='films'></films-list>

    <link rel="icon" href="/public/ghibli_logo.jpg"/>


  </div>
</template>

<script>
import ListComponent from './components/ListComponent.vue';
import FilmsList from './components/FilmsList.vue';
import FilmDetail from './components/FilmDetail.vue';
import FilmFilterForm from './components/FilmFilterForm.vue';
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
    "film-detail": FilmDetail,
    "film-filter-form": FilmFilterForm
  }
}
</script>

<style>

body {
  font-family: 'Trattatello', fantasy;
  background: url('https://i.pinimg.com/originals/04/7e/27/047e272b1f90381af4efcb115f6e1379.jpg') no-repeat center center fixed;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
}

h1 {
  text-align: center;
}

p {
}

div {
  color: white;
  text-align: center;
  display: inline-table;
  padding: inherit;
  text-indent: inherit;
}

</style>
