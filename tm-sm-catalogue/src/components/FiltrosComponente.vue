<template>
  <nav class="filtros">
    <h2> Filtros:</h2>
    <select v-model="selectedCategoria">
      <option value="">Todas las categorias</option>
      <option v-for="categoria in categorias" :key="categoria">{{ categoria}}</option>
    </select>
    <input type="number" v-model.number="precioMin" placeholder="Precio mínimo">
    <input type="number" v-model.number="precioMax" placeholder="Precio máximo">
    <button @click="aplicarFiltros">Aplicar filtros</button>
  </nav>
</template>

<script>

export default {
  data() {
    return {
      selectedCategoria: '',
      precioMin: null,
      precioMax: null
    };   
  },
  props: ['categorias'],
  methods: {
    aplicarFiltros() {
      this.$emit('filtrar', {categoria: this.selectedCategoria, precioMin: this.precioMin, precioMax: this.precioMax });
    }
  }
}
</script>

<style scoped>
  .filtros {
    margin-bottom: 20px;
  }
</style>
