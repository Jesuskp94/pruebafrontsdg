<template>
  <div>

    <select @change="eventoCambiarNumFilasTabla($event)">
        <option v-for="numRegistrosPagina in listaNumFilasPorPagina" :value="numRegistrosPagina.num" :key="numRegistrosPagina.id">{{ numRegistrosPagina.num }}</option>
    </select>
  </div>
</template>

<script>
    export default {
        name: 'dropDownMenu',
        data () {
            return {
                listaNumFilasPorPagina: [
                    { id: 1, num: 25},
                    { id: 2, num: 50},
                    { id: 3, num: 100},
                    { id: 4, num: 200}
                ]
            }
        },
        methods: {
            eventoCambiarNumFilasTabla(event)
            {
                let numPagina = parseInt(event.target.options[event.target.options.selectedIndex].value)
                this.$emit('cambiar-num-filas-tabla', numPagina)
            }
        }
    }
</script>