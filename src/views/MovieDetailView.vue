<template>
  <div>
    <div v-if="movie && !loading" class="movie-detail">
      <h2>{{ movie.Title }}</h2>
      <div class="flex">
        <img :src="movie.Poster" alt="Movie Poster" class="featured-img" />
        <div class="info">
          <div class="flex">
            <p>
              Year: <span>{{ movie.Year }}</span>
            </p>
            <p>
              Genre: <span>{{ movie.Genre }}</span>
            </p>
            <p>
              Rating: <span>⭐{{ movie.imdbRating }}</span>
            </p>
            <p>
              Country: <span>{{ movie.Country }}</span>
            </p>
            <p>
              Language: <span>{{ movie.Language }}</span>
            </p>
            <p>
              Actors: <span>{{ movie.Actors }}</span>
            </p>
          </div>
          <p>{{ movie.Plot }}</p>
        </div>
      </div>
    </div>

    <div v-else class="center">
      <LoaderComponent />
    </div>
  </div>
</template>

<script>
import LoaderComponent from '@/components/LoaderComponent.vue'
export default {
  name: 'MovieDetailView',
  components: { LoaderComponent },
  data() {
    return {
      movie: null,
      loading: true
    }
  },
  mounted() {
    fetch(`http://www.omdbapi.com/?apikey=e79d051&i=${this.$route.params.id}&plot=full`)
      .then((res) => res.json())
      .then((data) => {
        if (data) {
          this.loading = false
          this.movie = data
        }
      })
      .catch((e) => console.log(e))
  }
}
</script>

<style scoped>
.center {
  height: 90vh;
  display: grid;
  place-items: center;
}
.flex {
  width: 100%;
  display: flex;
  gap: 20px;
}
.movie-detail {
  padding: 16px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.info .flex {
  flex-direction: column;
  gap: 0px;
}
.info span {
  color: #42b883;
}
h2 {
  color: #42b883;
  font-size: 28px;
  font-weight: 600;
  margin-bottom: 16px;
  text-align: center;
}

.featured-img {
  display: block;
  max-width: 200px;
  margin-bottom: 16px;
}

p {
  color: #fff;
  font-size: 18px;
  line-height: 1.4;
}
@media only screen and (max-width: 768px) {
  .flex {
    flex-direction: column;
  }
}
</style>
