<template>{{ message }}</template>

<script>
  export default {

    data() {
      return {
        message: 'test'
      };
    },

    created() {
      $.getJSON('api/movies', function(data) {
        console.log(data);
      });
    }

  };
</script>
