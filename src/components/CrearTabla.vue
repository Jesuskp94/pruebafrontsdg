<template>
  <div class="row">
    <div class="col m12">
      <div class="table">
        <thead>
          <tr>
            <th scope="col">Titulo</th>
            <th scope="col">Año</th>
            <th scope="col">Director</th>
            <th scope="col">Casting</th>
            <th scope="col">Genero</th>
            <th scope="col">Notas</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="pelicula in leerDatos()" v-bind:key="pelicula.title">
            <th scope="row">{{ pelicula.title }}</th>
            <td>{{ pelicula.year }}</td>
            <td>{{ pelicula.director }}</td>
            <td>{{ pelicula.cast }}</td>
            <td>{{ pelicula.genre }}</td>
            <td>{{ pelicula.notes }}</td>
          </tr>
        </tbody>
      </div>
    </div>
  </div>
</template>

<script>
  import peliculas from "../assets/movies.json";

  export default {
    name: 'LeerDatos',
    methods: {
      leerDatos() {
        console.log("prueba");
        return peliculas.map(function(pelicula) {
          return pelicula;
        });
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.table {
  margin: 40px 0 0;
  border: 1px solid black;
  border-collapse: 1px solid black;
}
th, td {
  border-bottom: 1px solid #ddd;
  border-collapse: 1px solid #ddd;
}
</style> 