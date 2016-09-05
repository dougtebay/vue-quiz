<template>
  <p>{{ current_movie.id }} {{ current_movie.name }}</p>
  <button class="btn btn-primary" @click="getPreviousMovie()">{{ config.previous_button_text }}</button>
  <button class="btn btn-default" @click="getNextMovie()">{{ config.next_button_text }}</button>
</template>

<script>
  export default {
    data() {
      return {
        movies: [],
        current_movie: '',
        current_movie_index: 0,
        config: {
          previous_button_text: 'Previous',
          next_button_text: 'Next'
        }
      }
    },
    methods: {
      getMovies() {
        $.getJSON('api/movies', function(data) {
          this.movies = data.records
          this.setCurrentMovie()
        }.bind(this))
      },

      setCurrentMovie() {
        this.current_movie = this.movies[this.current_movie_index]
      },

      getPreviousMovie() {
        this.current_movie_index -= 1
        this.setCurrentMovie()
      },

      getNextMovie() {
        this.current_movie_index += 1
        this.setCurrentMovie()
      }
    },
    created() {
      this.getMovies()
    }
  }
</script>
