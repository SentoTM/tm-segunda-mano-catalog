<template>
  <div id="app">
    <filtros-componente :categorias="categorias" @filtrar="filtrarProductos"></filtros-componente>
    <div v-if="productosFiltrados.length > 0">
      <objeto-componente v-for="producto in productosFiltrados" :key="producto.id" :objeto="producto"></objeto-componente>
    </div>
    <div v-else>
      <p>No hay productos que coincidan con los filtros seleccionados.</p>
    </div>
  </div>
</template>

<script>
import productos from '../public/productos.json'
import FiltrosComponente from './components/FiltrosComponente.vue';
import ObjetoComponente from './components/ObjetoComponente.vue';

export default {
  name: 'App',
  components: {
    ObjetoComponente,
    FiltrosComponente
  },
  data() {
    return {
      productos: [],
      categorias: [],
      productosFiltrados: []
    };
  },
  mounted() {
    this.productos = productos;
    this.categorias= this.obtenerCategorias();
    this.productosFiltrados = [...this.productos];
  },
  methods: {
    obtenerCategorias() {
      const categoriasUnicas = new Set(this.productos.map(producto => producto.categoria));
      return Array.from(categoriasUnicas);
    },
    filtrarProductos(filtros) {
      this.productosFiltrados = this.productos.filter(producto => {
        return (!filtros.categoria || producto.categoria === filtros.categoria) &&
        (!filtros.precioMin || producto.precio >= filtros.precioMin) &&
        (!filtros.precioMax || producto.precio <= filtros.precioMax);
      });
    }
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
}
</style>
