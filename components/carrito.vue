<template>
    <div>
      <v-badge color="error" :content="productos.length" overlap>
        <v-btn icon @click="detalle">
          <v-icon>mdi-cart</v-icon>
        </v-btn>
      </v-badge>
  
      <factura 
        :show="show"
        :compras="productos"
        @cerrar="cerrar"
        @eliminar="emitirEliminar"
        @actualizarCantidad="emitirActualizarCantidad"
      ></factura>
    </div>
  </template>
  
  <script>
  import factura from './factura.vue';
  
  export default {
    components: { factura },
    props: {
      productos: {
        type: Array,
        default: () => []
      }
    },
    data() {
      return {
        show: false
      };
    },
    methods: {
      detalle() {
        this.show = true;
      },
      cerrar() {
        this.show = false;
      },
      emitirEliminar(index) {
        this.$emit('eliminar', index);
      },
      emitirActualizarCantidad(payload) {
        this.$emit('actualizarCantidad', payload);
      }
    }
  };
  </script>
  