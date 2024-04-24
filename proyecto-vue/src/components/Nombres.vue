<template>
  <div>
    Agregar Nombre:

    <form v-if="!mostrarEdicion" @submit.prevent="agregarNombre">

      <input type="text" v-model="nuevoNombre" placeholder="Nombre" required>

      <input type="text" v-model="nuevoApellido" placeholder="Apellido" required>

      <button type="submit">Agregar Nombre</button>

    </form>

    <div v-if="mostrarAdvertencia">Falta agregar mayusculas al nombre o apellido...</div>

    <ul>
      <li v-for="(nombre, index) in nombres" :key="index">
        {{ nombre.nombre }} {{ nombre.apellido }}
        <button @click="eliminarNombre(index)">Eliminar</button>
        <button @click="mostrarFormularioEdicion(index)">Editar</button>
      </li>
    </ul>

    <EditarNombre v-if="mostrarEdicion"
       :nombre="nombreEditado"
        @editar="guardarCambiosNombre"/>
  </div>
</template>

<script>
import EditarNombre from './EditarNombre.vue';

export default {
  name: 'ListaNombres',
  components: {
    EditarNombre
  },
  data() {
    return {
      nuevoNombre: '',
      nuevoApellido: '',
      nombres: [
        { nombre: 'Juanito', apellido: 'Juanin' },
        { nombre: 'Mari', apellido: 'A' }
      ],

      mostrarEdicion: false,
      nombreEditado: null,
      indiceEditar: null,
      mostrarAdvertencia: false 
    };
  },
  methods: {
    agregarNombre() {
      // Validar mayuscula
      if (!this.validarMayuscula(this.nuevoNombre) || !this.validarMayuscula(this.nuevoApellido)) {
        this.mostrarAdvertencia = true;
        return;
      }
      
      this.mostrarAdvertencia = false;
      this.nombres.push({ nombre: this.nuevoNombre, apellido: this.nuevoApellido });
      this.nuevoNombre = '';
      this.nuevoApellido = '';
    },

    validarMayuscula(cadena) {
      return /^[A-Z]/.test(cadena); 
    },

    eliminarNombre(index) {
      this.nombres.splice(index, 1);
    },

    mostrarFormularioEdicion(index) {
      this.nombreEditado = { ...this.nombres[index] };
      this.indiceEditar = index;
      this.mostrarEdicion = true;
    },

    guardarCambiosNombre(nombreEditado) {
      this.nombres.splice(this.indiceEditar, 1, nombreEditado);
      this.mostrarEdicion = false;
    }
  }
};
</script>
