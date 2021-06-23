<template>                                <!-- TODO: Meter bootstrap -->
  <div>
    <DropDown @cambiar-num-filas-tabla="cambiarNumFilasTabla"></DropDown>

    <table>
      <thead>
        <tr>
          <th v-for="columna in columnas" :key="columna.id" v-on:click="filtrarTabla(columna)">{{ columna }}
            <div class="flecha" v-if="columna == filtroColumna" v-bind:class="[ascendente ? 'flecha_arriba' : 'flecha_abajo']"></div>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="fila in get_filas()" :key="fila.id"> 
          <td v-for="columna in columnas" :key="columna.id">{{ fila[columna] }}</td>
        </tr>
      </tbody>
    </table>
    
    
  </div>
</template>

<script>
  import peliculas from "@/assets/movies.json"
  import DropDown from "@/components/DropDowns/DropDown.vue"
  // import BotonVolverArriba from "@/components/BotonVolverArriba.vue"


  export default {
    name: 'tablaPeliculas',
    data() {
      return {
        paginaActual: 1,
        numRegistrosPorPagina: 25,
        ascendente: false,
        filtroColumna: '',
        registros: peliculas
      }
    },
    components:{
      DropDown
    },
    methods: {
      filtrarTabla(columna) {
        if (this.filtroColumna === columna) {
          this.ascendente = !this.ascendente;
        } else {
          this.ascendente = true;
          this.filtroColumna = columna;
        }

        var ascendente = this.ascendente;

        this.registros.sort(function(colA, colB) {
          if (colA[columna] > colB[columna]) {
            return ascendente ? 1 : -1
          } else if (colA[columna] < colB[columna]) {
            return ascendente ? -1 : 1
          }
          return 0;
        })
      },
      cambiarNumFilasTabla(numero) {
        this.numRegistrosPorPagina = numero
        this.paginaActual = 1
      },
      num_paginas() {
        return Math.ceil(this.registros.length / this.numRegistrosPorPagina);
      },
      get_filas() {
        var inicio = (this.paginaActual-1) * this.numRegistrosPorPagina;
        var fin = inicio + this.numRegistrosPorPagina;
        return this.registros.slice(inicio, fin);
      },
    },
    computed: {
      columnas() {
        if (this.registros.length == 0) {
          return [];
        }
        return Object.keys(this.registros[0])
      }
    }
  }
</script>

<!--Borrar cuando haya metido bootstrap-->
<style scoped>


</style> 