<template>
  <h1>Listado</h1>
  <table>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Precio</th>
          <th>Stock</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="producto in products" :key="producto.id">
          <td>{{ producto.nombre }}</td>
          <td>{{ producto.precio }}</td>
          <td>{{ producto.stock }}</td>
        </tr>
      </tbody>
  </table>
</template>

<script>

  import {listenProducts} from '../firebase.js';

  export default {
    data() {
      return {
        nombre: '',
        precio: 0.0,
        stock: 0.0,
        products: [],
      };
    },
    mounted() {
      listenProducts(snapshot => {
        this.products = snapshot.docs.map(doc => ({ id: doc.id, ...doc.data() }));
      }, error => {
        console.error('Error escuchando productos:', error);
      });
    }
  };
  
</script>