<template>
    <div>
      <h2>Editar Nombre</h2>

      <form @submit.prevent="editarNombre">

        <input type="text" v-model="nombreEditado.nombre" placeholder="Nombre" required>

        <input type="text" v-model="nombreEditado.apellido" placeholder="Apellido" required>

        <button type="submit">Guardar Cambios</button>

      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: ['nombre'],
    data() {
      return {
        nombreEditado: { ...this.nombre } // Copia del nombre a editar
      };
    },
    methods: {
      editarNombre() {
        this.$emit('editar', this.nombreEditado);
      }
    }
  };
  </script>
  