<template>
  <div class="container">
    <div class="card text-center">
      <div class="card-header">Productos</div>
      <div class="card-body">
        <table class="table">
          <thead>
            <tr>
              <th scope="col">ID</th>
              <th scope="col">CATEGORIA</th>
              <th scope="col">NOMBRE</th>
              <th scope="col">REFERENCIA</th>
              <th scope="col">PRECIO</th>
              <th scope="col">STOCK</th>
              <th scope="col">ACCIONES</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="producto in productos" :key="producto.id">
              <th scope="row">{{ producto.id }}</th>
              <td>{{ producto.category }}</td>
              <td>{{ producto.name }}</td>
              <td>{{ producto.reference }}</td>
              <td>{{ producto.price }}</td>
              <td>{{ producto.stock }}</td>
              <td>
                <router-link :to="{name:'Editar', params:{id:producto.id}}" class="btn btn-primary">editar</router-link>
                <button
                  class="btn btn-danger"
                  v-on:click="this.borrarProducto(producto.id)"
                >
                  eliminar
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      productos: [],
    };
  },
  created: function () {
    this.consultarProductos();
  },
  methods: {
    borrarProducto(id) {
      const optionsRequest = {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
        },
      };

      fetch("http://localhost:8000/api/product_delete/" + id, optionsRequest)
        .then((response) => response.json())
        .then((data) => {
          console.log(data);
          window.location.href = "listar";
        })
        .catch(console.log);
    },

    async consultarProductos() {
      this.productos = [];

      const optionsRequest = {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
        },
      };

      const response = await fetch(
        `http://localhost:8000/api/product_index`,
        optionsRequest
      );
      const data = await response.json();

      if (typeof data !== "undefined") {
        this.productos = data;
      }
    },
  },
};
</script>