<template>
  <v-dialog v-model="mostrar" width="auto" persistent>
    <v-card max-width="500" title="Productos Comprados">
      <v-card-text>
        <div v-for="(producto, index) in compras" :key="index">
          <v-card outlined class="mb-4 d-flex justify-space-between">
            <div class="d-flex">
              <v-img :src="producto.imagen" height="150px" width="100px"></v-img>

              <div class="ml-4">
                <v-card-title>{{ producto.titulo }}</v-card-title>
                <v-card-subtitle>{{ producto.descripcion }}</v-card-subtitle>
                <v-card-text>Precio: ${{ producto.precio }}</v-card-text>
                <div class="d-flex align-center">
                  <v-btn 
                    small 
                    icon 
                    @click="decrementarCantidad(index)"
                    :disabled="producto.cantidad <= 1"
                  >
                    <v-icon>mdi-minus</v-icon>
                  </v-btn>
                  <span class="mx-2">{{ producto.cantidad }}</span>
                  <v-btn small icon @click="incrementarCantidad(index)">
                    <v-icon>mdi-plus</v-icon>
                  </v-btn>
                  <v-btn 
                    color="error" 
                    class="ml-4" 
                    @click="eliminarProducto(index)"
                    icon
                    density="comfortable"
                  >
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </div>
              </div>
            </div>
            <v-btn icon color="red" @click="eliminarProducto(index)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-card>
        </div>
      </v-card-text>
      
      <v-card-text class="d-flex justify-end">
        <div class="text-h6">
          Total: ${{ calcularTotal }}
        </div>
      </v-card-text>

      <v-card-actions>
        <v-btn class="ms-auto" text @click="cerrar">Cerrar</v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    },
    compras: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      mostrar: false
    };
  },
  methods: {
    cerrar() {
      this.$emit('cerrar');
    },
    eliminarProducto(index) {
      this.$emit('eliminar', index);
    },
    incrementarCantidad(index) {
      this.$emit('actualizarCantidad', { index, cambio: 1 });
    },
    decrementarCantidad(index) {
      if (this.compras[index].cantidad > 1) {
        this.$emit('actualizarCantidad', { index, cambio: -1 });
      }
    }
  },
  watch: {
    show(newVal) {
      this.mostrar = newVal;
    }
  },
  computed: {
    calcularTotal() {
      return this.compras.reduce((total, producto) => {
        return total + (producto.precio * producto.cantidad)
      }, 0).toFixed(2)
    }
  }
};
</script>
