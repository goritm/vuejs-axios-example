<template>
  <div class="container-fluid" id="app">
    <h1 align="center">Consumo de API con Vue.js y Axios</h1>
    <h2 align="center">Jose Sandoval</h2>

    <form @submit.prevent="leerAPI">
      <div class="form-group">
        <label>¿Cuantos resultados desea?</label>
        <div class="input-group">
          <input class="form-control" v-model="cantidadResultados">
          <button class="btn btn-dark" type="submit">OK</button>
        </div>
      </div>
    </form>

    <table class="table table-striped">
      <thead class="thead-dark">
        <tr>
          <th>Titulo</th>
          <th>Descripcion</th>
          <th>Director</th>
          <th>Fecha de lanzamiento</th>
          <th>Puntuación</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="movie in movies">
          <!-- <td>{{ movie }}</td> -->
          <td>{{ movie.title }}</td>
          <td>{{ movie.description }}</td>
          <td>{{ movie.director }}</td>
          <td>{{ movie.release_date }}</td>
          <td>{{ movie.rt_score }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "app",
  data() {
    return {
      movies: [],
      cantidadResultados: 5,
      puntuacionPedida: 80,
      url: "https://ghibliapi.herokuapp.com/films"
    };
  },
  created() {
    this.leerAPI();
  },
  // computed: {
  //   peliculasBuenas: function() {
  //     return this.movies.filter(function(u) {
  //       return u.rt_score >= 97;
  //     });
  //   }
  // },
  methods: {
    leerAPI() {
      axios
        .get(this.url, {
          params: {
            limit: this.cantidadResultados
          }
        })
        .then(response => {
          this.movies = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>