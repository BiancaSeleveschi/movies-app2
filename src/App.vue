<template>
  <div id="app">
    <h1>FILME</h1>
    <div class="input-group mb-3" >
      <input v-model="movieSearched.title" type="text" class="form-control w-auto" placeholder="Numele filmului">
      <button class="btn btn-secondary">Search</button>
      <div>{{ movieSearched }}</div>
    </div>
    <div class=" p-2 m-auto">
      <input v-model="newMovie.title" type="text" placeholder="Numele filmului">
      <input v-model="newMovie.gendre" type="text" placeholder="Gen">
      <input v-model="newMovie.producer" type="text" placeholder="Regizor">
      <input v-model="newMovie.year" type="text" placeholder="Anul aparitiei">
      <input v-model="newMovie.seen" type="text" placeholder="Vazut">
      <button @click="addNewMovie">Adauga film</button>
    </div>

    <h2 class="p-3" @click="showMovie = !showMovie">Lista de filme</h2>
    <div v-show="showMovie">
      <div v-for="(movie, index) in movies" v-bind:key="index" id="movies-div"
           class="col border border-3 border border-dark rounded-4 m-auto p-3 text-dark fst-italic my-2">
        <p @click="showIndexDetails = showIndexDetails === -1 ? index : -1"> {{ movie.title }}</p>
        <div v-show="showIndexDetails === index">
          <p>Genul: {{ movie.gendre }}</p>
          <p>Producator: {{ movie.producer }}</p>
          <p>Anul aparitiei: {{ movie.year }}</p>
          <p>Vazut: {{ movie.seen }}</p>
          <button @click="seenButton = !seenButton" class="btn btn-warning mx-2">{{
              seenButton ? "✔️" : "Seen"
            }}
          </button>
          <button @click="deleteMovie" class="btn btn-success">Delete</button>
          <div v-show="seenButton">
            <input v-model="seenInput" class="my-2" type="number" placeholder="year">
            <p>{{ seenInput }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      movies: [
        {
          title: "Se7en",
          gendre: "Drama",
          producer: "James Mc. Teigue",
          year: 2000,
          seen: false
        },
        {
          title: "Blood Diamond",
          gendre: "Drama",
          producer: "Edward Zwik",
          year: 2007,
          seen: false
        },
        {
          title: "Changeling",
          gendre: "Mister",
          producer: "Clint Eastwood",
          year: 2011,
          seen: false
        },
        {
          title: "Alive",
          gendre: "Aventura",
          producer: "Franc Marshall",
          minutesLength: 127,
          year: 2005,
          seen: true
        }
      ],
      newMovie: {
        title: "",
        gendre: "",
        producer: "",
        year: '',
        seen: '',
      },
      movieSearched: "",
      showMovie: false,
      showIndexDetails: -1,
      seenButton: false,
      seenInput: '',
      showSeenMovie: false,
      showIndexInput: -1,
    }
  },
  methods: {
    addNewMovie() {
      this.movies.push(this.newMovie)
    },
    deleteMovie(index) {
      this.movies.splice(index, 1)
      this.showIndexDetails = this.showIndexDetails === -1 ? index : -1;
    },
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: cornflowerblue;
}

html {
  background: lavenderblush;
}

#movies-div {
  background: blue;
  width: 350px;
}

p {
  color: cornsilk;
}
</style>
