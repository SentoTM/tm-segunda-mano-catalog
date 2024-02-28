<template>
  <article class="objeto">
    <img :src="objeto.imagen" alt="objeto.descripcion">
    <h3>{{ objeto.nombre }}</h3>
    <p>Categoría: {{ objeto.categoria }}</p>
    <p>Precio: {{ objeto.precio }}</p>
    <p>{{ objeto.descripcion }}</p>
  </article>
</template>

<script>
  export default {
    props: [objeto]
  }
</script>

<style scoped>
  .objeto {
    margin-bottom: 20px;
  }
</style>
