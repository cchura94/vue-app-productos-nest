<script setup>
import axios from "axios"
import { ref } from "vue";

const productos = ref([]);
const producto = ref({})

async function getProductos(){
  const respuesta = await axios.get("http://127.0.0.1:3000/producto")
  console.log(respuesta.data);
  productos.value = respuesta.data
}

getProductos();

async function funGuardarProducto(){
  const res = await axios.post("http://127.0.0.1:3000/producto", producto.value);
  getProductos();
}

</script>

<template>
  <div>
    <h1>Nuevo Producto</h1>
    <label for="n">Ingrese Nombre</label>
    <input type="text" v-model="producto.nombre">
    <br>
    <label for="precio">Ingrese Precio</label>
    <input type="text" v-model="producto.precio">
    <br>
    <label for="cant">Ingrese Cantidad</label>
    <input type="text" v-model="producto.cantidad">
    <br>
    <label for="img">Ingrese Imagen</label>
    <input type="text" v-model="producto.imagen">
    <br>
    <button @click="funGuardarProducto()">Guardar Producto</button>
  </div>
  {{ producto }}
  <h1>Lista de Productos</h1>


  <table border="1">
    <thead>
      <tr>
        <th>ID</th>
        <th>NOMBRE</th>
        <th>PRECIO</th>
        <th>CANTIDAD</th>
        <th>IMAGEN</th>
        <th>ACCIONES</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="prod in productos">
        <td>{{ prod.id }}</td>
        <td>{{ prod.nombre }}</td>
        <td>{{ prod.precio }} USD</td>
        <td>{{ prod.cantidad }}</td>
        <td>
          <img :src="prod.imagen" alt="" width="100px">
        </td>
        <td>
          <button>x</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
