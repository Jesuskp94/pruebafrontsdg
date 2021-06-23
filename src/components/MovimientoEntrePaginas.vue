<template>

  <div class="pagination" v-if="numPaginas > 10">
    <button v-on:click="$emit('pag-anterior')">Anterior</button>
    <span> Pag {{ paginaActual }} de {{ numPaginas }}</span>
    <button v-on:click="$emit('pag-siguiente')">Siguiente</button>
  </div>

  <div v-else>
   <div class="number"
     v-for="i in numPaginas" :key="i"
     :class="[i == paginaActual ? 'active' : '']"
     v-on:click="emitirEventoIrPagina(i)">
     {{ i }}
   </div>
 </div>
</template>

<script>
    export default {
      name: 'MovimientoEntrePaginas',
      methods: {
        emitirEventoIrPagina(indice) {
          this.$emit('pasar-pagina', indice)
        }
      },
      props: {
        numPaginas: {
          type: Number,
          required: true
        },
        paginaActual: {
          type: Number,
          required: true
        }
      }
    }
</script>