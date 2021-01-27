<template>
  <div class="content">
    <table class="table">
      <thead>
        <tr>
          <th scope="col">Nombre</th>
          <th scope="col">Nota</th>
          <th scope="col">Descripcion</th>
          <th scope="col">Fecha</th>
          <th scope="col">Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in notas" :key="index">
          <td>{{ item.nombre }}</td>
          <td>{{ item.nota }}</td>
          <td>{{ item.descripcion.toUpperCase() }}</td>
          <td>{{ item.date }}</td>
          <td>
            <b-button
              class="btn-warning btn-sm mx-2"
              @click="activarEdicion(item._id)"
              >Actualizar</b-button
            >
            <b-button
              class="btn-danger btn-sm mx-2"
              @click="eliminarNota(item._id)"
              >Eliminar</b-button
            >
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      notas: [],
      mensaje: { color: "success", texto: "" },
      dismissSecs: 5,
      dismissCountDown: 0,
    };
  },
  created() {
    this.listarNotas();
  },
  methods: {
    listarNotas() {
      this.axios
        .get("nota")
        .then((response) => {
          // console.log(result.data);
          this.notas = response.data;
        })
        .catch((e) => {
          console.log("error" + e);
        });
    },
    countDownChange(dismissCountDown) {
      this.dismissCountDown = dismissCountDown;
    },
    showAlert() {
      this.dismissCountDown = this.dismissSecs;
    },
  },
};
</script>

