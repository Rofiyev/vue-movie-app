<template>
  <section class="home">
    <div class="cards">
      <div v-for="movie in defaultMovies" :key="movie" class="feature-card">
        <RouterLink :to="{ name: 'movie-detail', params: { id: movie.imdbID } }">
          <img :src="movie.Poster" alt="Naruto Poster" class="featured-img" />
          <div class="detail">
            <h3>{{ movie.Title }}</h3>
            <h4>{{ movie.Year }}</h4>
            <p>
              A pair of teenagers with cystic fibrosis meet in a hospital and fall in love, though
              their disease means they must avoid close physical contact.
            </p>
          </div>
        </RouterLink>
      </div>
    </div>
    <form @submit.prevent="handleSubmit" class="search-box">
      <input type="text" placeholder="What are you looking for?" v-model="search" />
      <input type="submit" value="Search" />
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="movie.imdbID">
        <RouterLink :to="{ name: 'movie-detail', params: { id: movie.imdbID } }" class="movie-link">
          <div class="product-image">
            <img :src="movie.Poster" alt="Movie Poster" />
            <div class="type">{{ movie.Type }}</div>
          </div>
          <div class="detail">
            <p class="year">{{ movie.Year }}</p>
            <h3>{{ movie.Title }}</h3>
          </div>
        </RouterLink>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      search: '',
      movies: [],
      defaultMovies: []
    }
  },
  methods: {
    handleSubmit() {
      if (this.search) {
        fetch(`http://www.omdbapi.com/?apikey=e79d051&s=${this.search}`)
          .then((res) => res.json())
          .then((data) => (this.movies = data.Search))
      }
      this.search = ''
    }
  },
  mounted() {
    fetch(`http://www.omdbapi.com/?apikey=e79d051&s=five%20five%20apart`)
      .then((res) => res.json())
      .then((data) => (this.defaultMovies = data.Search))
  }
}
</script>

<style scoped>
.home {
  max-width: 1200px;
  margin: 0 auto;
}
.cards {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 20px;
  margin: 10px auto;
}
.feature-card {
  position: relative;
  flex-basis: 350px;
}
.featured-img {
  display: block;
  height: 450px;
  width: 100%;
  object-fit: cover;

  position: relative;
  z-index: 0;
}
.feature-card .detail {
  position: absolute;
  width: 100%;
  left: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.6);
  z-index: 1;
  padding: 1rem;
}
.feature-card .detail h3 {
  color: white;
}
.feature-card .detail h4 {
  color: white;
  margin-bottom: 1rem;
}
.feature-card .detail p {
  color: white;
}
.search-box {
  display: flex;
  gap: 10px;
  justify-content: center;
  padding: 1rem;
  align-items: center;
}
.search-box input {
  display: block;
  appearance: none;
  border: none;
  outline: none;
  background: none;
}
.search-box input[type='text'] {
  width: 100%;
  background-color: #496583;
  color: white;
  font-size: 1.2rem;
  padding: 10px 16px;
  border-radius: 8px;
}
.search-box input[type='text']::placeholder {
  color: #f3f3f3;
}
.search-box input[type='text']:focus {
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.2);
}
.search-box input[type='submit'] {
  width: 100%;
  max-width: 200px;
  background-color: #42b883;
  padding: 10px 0;
  border-radius: 8px;
  color: #fff;
  font-size: 20px;
  text-transform: uppercase;
  transition: 0.4s;
}
.search-box input[type='submit']:active {
  background-color: #3b8070;
}
.movies-list {
  display: flex;
  flex-wrap: wrap;
  margin: 0px 8px;
}
.movies-list .movie {
  max-width: 50%;
  flex: 1 1 50%;
  padding: 16px 8px;
}
.movies-list .movie .movie-link {
  display: flex;
  flex-direction: column;
  height: 100%;
  text-decoration: none;
}
.movies-list .movie .movie-link .product-image {
  position: relative;
  display: block;
}
.movies-list .movie .movie-link .product-image img {
  display: block;
  width: 100%;
  height: 275px;
  object-fit: cover;
}
.movies-list .movie .movie-link .product-image .type {
  position: absolute;
  padding: 8px 16px;
  background-color: #42b883;
  color: #fff;
  bottom: 16px;
  left: 0px;
  text-transform: capitalize;
}
.movies-list .movie .movie-link .detail {
  background-color: #496583;
  padding: 16px 8px;
  flex: 1 1 100%;
  border-radius: 0px 0px 8px 8px;
}
.movies-list .movie .movie-link .detail .year {
  color: #aaa;
  font-size: 14px;
}
.movies-list .movie .movie-link .detail h3 {
  color: #fff;
  font-weight: 600;
  font-size: 18px;
}
</style>
