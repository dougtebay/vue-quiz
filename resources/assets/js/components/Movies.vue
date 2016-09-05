<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <div class="panel panel-default">
          <div class="panel-body">
            <p>Name: {{ current_movie.name }}</p>
            <p>Release date: {{ current_movie.release_date }}</p>
            <p>Synopsis: {{ current_movie.synopsis }}</p>
            <ul>
              <li v-for="actor in current_movie.actors">
                {{ actor }}
              </li>
            </ul>
          </div>
        </div>
        <button
          v-on:click="getPreviousMovie()"
          v-bind:class="{ 'current': config.previous_button_current }"
          v-bind:disabled="current_movie_index === 0"
          class="btn btn-primary">
          {{ config.previous_button_text }}
        </button>
        <button
          v-on:click="getNextMovie()"
          v-bind:class="{ 'current': config.next_button_current }"
          v-bind:disabled="current_movie_index === movies.length - 1"
          class="btn btn-primary">
          {{ config.next_button_text }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        movies: [],
        current_movie: '',
        current_movie_index: 0,
        current_button: false,
        config: {
          previous_button_text: 'Previous',
          next_button_text: 'Next',
          previous_button_current: false,
          next_button_current: false
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
        if(this.current_movie_index > 0) {
          this.current_movie_index -= 1
          this.setCurrentMovie()
          this.config.previous_button_current = true
          this.config.next_button_current = false
        }
      },

      getNextMovie() {
        if(this.current_movie_index < this.movies.length - 1) {
          this.current_movie_index += 1
          this.setCurrentMovie()
          this.config.next_button_current = true
          this.config.previous_button_current = false
        }
      }
    },
    created() {
      this.getMovies()
    }
  }
</script>
