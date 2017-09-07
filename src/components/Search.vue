<template>
  <v-container>
    <v-layout row>
      <v-flex xs8 offset-xs2>

<div class="mt-5">
  <h4>{{ search }}</h4>
  <p>Enter a search term like moon, rings or Neptune in the field below. The NASA API will show you images related to your query.</p>
    <form v-on:submit.prevent="getResult(query)" class="form-control">
      <v-text-field
              name="query"
              label="Type in your search"
              single-line
              v-model="query"
            ></v-text-field>

       <v-btn light v-on:click="getResult(query)">Enter</v-btn>
    </form>
    <div class="results" v-if="results">
      <div v-for="result in results">
        <img v-bind:src="result.links[0].href" />
      </div>
    </div>
</div>
</v-flex>
</v-layout>
</v-container>
</template>

<script>
import axios from 'axios'

export default {
  name: 'search',
  data () {
    return {
      search: 'WELCOME TO THE NASA SEARCH API',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult(query){
      axios.get('https://images-api.nasa.gov/search?q='+query+'&media_type=image').then(response => {
        //console.log(response.data.collection.items)
        this.results = response.data.collection.items
        this.query = ''
      })

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.results img{
  height: 300px;
  margin: 10px;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
