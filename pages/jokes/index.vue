<template>
    <div>
        <SearchJokes v-on:search-text="searchText"/>
        <Joke v-for="joke in jokes" v-bind:key="joke.id" :id="joke.id" :joke="joke.joke" />
    </div>
</template>

<script>
import axios from 'axios';
import Joke from '../../components/Joke';
import SearchJokes from '../../components/SearchJokes';

export default {
  data() {
      return {
          jokes: []
      }
  },
  components: {
      Joke,
      SearchJokes
  },
  async created() {
    const config = {
        headers: {
            'Accept': 'application/json'
        }
    }

    try  {
        const response = await axios.get('https://icanhazdadjoke.com/search', config);
        
        this.jokes = response.data.results;
    } catch (err) {
        console.log(err);
    }

  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
            'Accept': 'application/json'
        }
      }

      try  {
          const response = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config);
          
          this.jokes = response.data.results;
      } catch (err) {
          console.log(err);
      }
    }
  },
  head() {
    return {
      title: 'Dad Jokes',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for corny dad jokes'
        }
      ]
    }
  }
}
</script>

<style>

</style>
