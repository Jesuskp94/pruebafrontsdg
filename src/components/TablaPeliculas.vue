<template>                                <!-- TODO: Meter bootstrap -->
  <div>
    <DropDown @cambiar-num-filas-tabla="cambiarNumFilasTabla"></DropDown>

    <!-- Preguntar por qué una llamada a un método no debe tener los parentesis (aunque reciba parámetros desde el componente hijo),
    y otra los exiga para hacer referencia al método (supongo que será por el bind pero no lo tengo claro) -->
    <MovimientoEntrePaginas @pag-anterior="retrocederPagina" @pag-siguiente="pasarPagina" @pasar-pagina="cambiarPagina" :numPaginas="num_paginas()" :paginaActual="paginaActual"></MovimientoEntrePaginas>

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
  import MovimientoEntrePaginas from "@/components/MovimientoEntrePaginas.vue"
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
      DropDown,
      MovimientoEntrePaginas,
    },
    methods: {
      filtrarTabla(columna) {
        if (this.filtroColumna === columna) {
          this.ascendente = !this.ascendente;
        } else {
          this.ascendente = true;
          this.filtroColumna = columna;
        }

        this.paginaActual = 1
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
      pasarPagina() {
        if(this.paginaActual < this.num_paginas()) {
          this.paginaActual +=1
        }
      },
      retrocederPagina() {
        if(this.paginaActual > 1){
          this.paginaActual -=1
        }
      },
      cambiarPagina(pagina) {
        this.paginaActual = pagina;
      }
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