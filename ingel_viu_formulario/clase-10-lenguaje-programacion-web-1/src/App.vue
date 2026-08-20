<script setup>
import { ref } from "vue";
import Title from "./components/Title.vue";

// Datos iniciales del almacén
const products = ref([
  { product: "Arroz", quantity: 25, location: "Pasillo A" },
  { product: "Aceite", quantity: 15, location: "Pasillo B" },
  { product: "Leche", quantity: 30, location: "Pasillo C" },
]);

const product = ref("");
const quantity = ref("");
const location = ref("");

const show = ref(false);
const buttonTitle = ref("Mostrar");

function mostrarDatos() {
  show.value = !show.value;

  if (show.value) {
    buttonTitle.value = "Ocultar";
  } else {
    buttonTitle.value = "Mostrar";
  }
}

function IngresarDato() {
  products.value.push({
    product: product.value,
    quantity: quantity.value,
    location: location.value,
  });

  product.value = "";
  quantity.value = "";
  location.value = "";
}
</script>

<template>
  <div class="contenedor">
    <Title />

    <h2>Registro de Almacén</h2>

    <form @submit.prevent="IngresarDato">
      <input
        type="text"
        placeholder="Nombre del producto"
        v-model="product"
      />

      <input
        type="number"
        placeholder="Cantidad"
        v-model="quantity"
      />

      <input
        type="text"
        placeholder="Ubicación"
        v-model="location"
      />

      <button type="submit">Ingresar</button>
    </form>

    <hr />

    <button @click="mostrarDatos">
      {{ buttonTitle }}
    </button>

    <table v-if="show">
      <thead>
        <tr>
          <th>Producto</th>
          <th>Cantidad</th>
          <th>Ubicación</th>
        </tr>
      </thead>

      <tbody>
        <tr v-for="product in products">
          <td>{{ product.product }}</td>
          <td>{{ product.quantity }}</td>
          <td>{{ product.location }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.contenedor {
  min-height: 100vh;
  background-color: aqua;

  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  text-align: center;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  width: 250px;
  margin-bottom: 20px;
}

input,
button {
  padding: 10px;
}

table {
  margin-top: 20px;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid black;
  padding: 10px 20px;
}
</style>