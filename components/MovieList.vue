<template>
  <main>
    <Search @onChildToParent="onChildClick" />
    <div class="movie-listing-container">
      <div class="movie-result-container">
        <ul class="movie-listing">
          <li
            v-for="movie in movies.slice(0, 1)"
            :key="movie.movies"
            class="movie-listing-item"
          >
            <Movie class="result-movie" :movie="movie" @addMovie="addToList" />
          </li>
        </ul>
      </div>
      <div class="watch-list-container">
        <h2 class="movie-listing__heading">Gotta See These</h2>
        <ul class="movie-listing watch-list">
          <li
            v-for="movie in watchList"
            :key="movie.movies"
            class="movie-listing-item"
          >
            <Movie
              class="watch-list-movie"
              :movie="movie"
              @removeMovie="removeFromList"
            />
          </li>
        </ul>
      </div>
    </div>
  </main>
</template>

<script>
const axios = require('axios')

export default {
  name: 'MovieList',
  components: {
    Movie: () => import('./Movie'),
    Search: () => import('./Search'),
  },
  data() {
    return {
      movies: [],
      searchQuery: '',
      watchList: [
        {
          poster_path: '/7lTfTZ8CDfXw09eAv3OOvsbCVgs.jpg',
        },
        {
          poster_path: '/j2KXt3gObsAaRj9RKpCp8tiosTk.jpg',
        },
        {
          poster_path: '/cUvdzCbhLyYUAwbIkBjT3tC28cK.jpg',
        },
        {
          poster_path: '/JC8KQ2BXaAIFEU8zEuakiwUQSr.jpg',
        },
      ],
    }
  },
  methods: {
    async fetchData() {
      try {
        const response = await axios.get(
          `https://api.themoviedb.org/3/search/movie?api_key=3e176f464be990c4b8fefff841cef7b4&language=en-US&query=${this.searchQuery}&page=1&include_adult=false`
        )
        const movies = await response.data
        this.movies = movies.results
      } catch (error) {
        console.error(error)
      }
    },
    onChildClick(value) {
      this.searchQuery = value
      this.fetchData()
    },
    addToList(movie) {
      const movieToAdd = {
        poster_path: movie.poster_path,
      }
      this.watchList.push(movieToAdd)
    },
    removeFromList(movie) {
      const index = this.watchList.indexOf(movie)
      this.watchList.splice(index, 1)
    },
  },
}
</script>

<style lang="scss">
.movie-listing-container {
  padding-top: 2rem;
  display: grid;
  grid-template-columns: 30% 1fr;
  @media only screen and (max-width: 850px) {
    grid-template-columns: 1fr;
  }
}

.movie-listing .movie-listing-item {
  list-style-type: none;
}

.result-movie {
  .c-movie-image {
    width: 11rem;
  }
}

.watch-list-movie {
  .c-movie-image {
    width: 8rem;
  }
}

.movie-listing {
  display: grid;
  list-style: none;
  padding: 1rem;
  margin: 0;
  grid-row-gap: 1rem;
}
.movie-listing__heading {
  color: white;
  text-align: center;
}

.watch-list {
  grid-template-columns: repeat(4, 1fr);
  @media only screen and (max-width: 600px) {
    grid-template-columns: repeat(3, 1fr);
  }
  @media only screen and (max-width: 450px) {
    grid-template-columns: repeat(2, 1fr);
  }
}

h2 {
  font-size: 2rem;
}
</style>
