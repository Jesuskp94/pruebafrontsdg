<template>
  <div class="row">
    <div class="col m12">
      <table>
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
            <td scope="row">{{ pelicula.title }}</td>
            <td scope="row">{{ pelicula.year }}</td>
            <td scope="row">{{ pelicula.director }}</td>
            <td scope="row">{{ pelicula.cast }}</td>
            <td scope="row">{{ pelicula.genre }}</td>
            <td scope="row">{{ pelicula.notes }}</td>
          </tr>
        </tbody>
      </table>
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
table {
  margin: 40px 40px 40px;
  border: 1px solid black;
  border-collapse: collapse;
}
th{
  background-color: #04AA6D;
  color: white;
}
th, td{
  border: 1px solid black;
}
</style> 