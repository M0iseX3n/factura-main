<template>
   <div>
     <cabezote
       :productos="comprasrealizadas"
       @eliminar="eliminarProducto"
       @actualizarCantidad="actualizarCantidad"
     ></cabezote>
     <manager
       :productos="productos"
       @compra="compra"
     ></manager>
   </div>
 </template>
 
 <script>
 import cabezote from '~/components/cabezote.vue';
 import manager from '~/components/manager.vue';
 
 export default {
   components: { cabezote, manager },
   data() {
     return {
       comprasrealizadas: [],
       productos: [
            {
                imagen : 'https://img.freepik.com/foto-gratis/zapatos-cuero-marron_1203-8175.jpg',
                precio :  220,
                titulo : 'Zapato clasico ',
                descripcion : 'Es el complemento ideal para un estilo sofisticado y elegante.'
            },
             {
                imagen : 'https://http2.mlstatic.com/D_696111-MLA70741601961_072023-C.jpg',
                precio : 150,
                titulo : 'zapato juvenil',
                descripcion : 'Su diseño versátil y cómodo es perfecto para cualquier ocasión.',

             } ,
             {
                imagen : 'https://azzurry.com/wp-content/uploads/2023/10/0251_BQ6806-122.jpg',
                precio : 125,
                titulo : 'Nike Blazer',
                descripcion : 'Los Nike Blazer son un ícono de la moda urbana y deportiva.',

             } ,
             {
                imagen : 'https://d2cva83hdk3bwc.cloudfront.net/onitsuka-tiger-mexico-66-yellow-black-1.jpg',
                precio : 184,
                titulo : 'Onitsika tiger mexico 66',
                descripcion : 'Son la combinación perfecta de estilo retro y comodidad moderna.',

             } ,
             {
                imagen : 'https://assets.adidas.com/images/h_840,f_auto,q_auto,fl_lossy,c_fill,g_auto/3bbecbdf584e40398446a8bf0117cf62_9366/Tenis_Samba_OG_Blanco_B75806_01_standard.jpg',
                precio : 200,
                titulo : 'Adidas Samba',
                descripcion : 'Un verdadero clásico de Adidas una mezcla perfecta de estilo y funcionalidad.',

             } ,
             {
                imagen : 'https://pufferreds.com/cdn/shop/files/A07893C-1.png?v=1714629148',
                precio : 150,
                titulo : 'Converse one star',
                descripcion : 'Aportan un toque clásico y atemporal a cualquier look.',

             } ,

          ]                   
           
        }
    },
    methods: {
    compra(data) {
      const productoExistente = this.comprasrealizadas.find(
        (producto) => producto.titulo === data.titulo
      );

      if (productoExistente) {
        return;
      }

      this.comprasrealizadas.push({ ...data, cantidad: 1 });
    },
    eliminarProducto(index) {
      this.comprasrealizadas.splice(index, 1);
    },
    actualizarCantidad({ index, cambio }) {
      // Accede al producto por índice
      const producto = this.comprasrealizadas[index];

      // Si no existe el producto, sal del método
      if (!producto) return;

      // Incrementa o disminuye la cantidad
      producto.cantidad += cambio;

      // Si la cantidad es 0 o menor, elimina el producto
      if (producto.cantidad <= 0) {
        this.eliminarProducto(index);
      }
    },
  }
};
</script>

<style>
.vivi {
   padding:30px ;
   background-color: #333;
   color:#000
}
</style>