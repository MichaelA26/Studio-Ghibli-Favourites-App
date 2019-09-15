<template lang="html">
  <article v-if="film">
    <p>Title: {{ film.title }}</p>
    <p>Description: {{ film.description }}</p>
    <p>Producer: {{ film.producer }}</p>
    <p>Release Year: {{ film.release_date }}</p>
  </article>
</template>

<script>
export default {
  name: 'film-detail',
  props: ['film']
}
</script>

<style lang="css" scoped>

</style>
