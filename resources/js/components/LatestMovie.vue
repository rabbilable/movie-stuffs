<template>
  <div id="latest">
  <div v-if="loading" class="loader"></div>
  <div v-for="items in totalResponses" :key="items.id">
    <div class="movie-section p-3" v-for="totalResponse in   items" :key="totalResponse.id">
      <div class="demo-card-wide mdl-card mdl-shadow--2dp" v-bind:style="{ 'background-image': 'url(' + `https://image.tmdb.org/t/p/w500${totalResponse.poster_path}` + ')' }" >
        <div class="mdl-card__title">
          <h1 class="mdl-card__title-text text-light"><strong>{{totalResponse.title}}</strong></h1>
        </div>
        <div class="mdl-card__supporting-text text-light">
          {{totalResponse.overview}}
        </div>
        <div class="mdl-card__actions mdl-card--border">
          <a class="mdl-button mdl-button--colored mdl-js-button mdl-js-ripple-effect text-light bg-dark" @click="singleMovie(totalResponse.id)">Get Details</a>
        </div>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function() {
    return {
      api_key: '5f5cc4cec8c4b74023cc7963417ca5d2',
      movie: 'https://api.themoviedb.org/3/movie/upcoming',
      totalResponses: [],
      loading: true
    };
  },

  mounted() {
    axios
      .get(
        `${this.movie}?api_key=${this.api_key}&language=en-US&page=1`
      )
      .then(res => {
        this.totalResponses = res.data
        this.loading = false
      })
      .catch(err => console.log(err));
  },
  methods: {
    singleMovie (id) {
      this.$router.push('/movie/' + id)
    }
  }
};
</script>

<style scoped>

.demo-card-wide.mdl-card {
  width: 500px;
}
.demo-card-wide > .mdl-card__title {
  color: #fff;
  height: 500px;
}
.demo-card-wide > .mdl-card__menu {
  color: #fff;
}
.loader {
  width: 120px;
  height: 120px;
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid black; /* Blue */
  border-radius: 50%;
  animation: spin 2s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>