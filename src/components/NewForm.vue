<template>
  <div class="form-container">
    <h2>Registro de datos</h2>
    <form @submit.prevent="submitForm">
      <div class="form-group">
        <label for="nombre">Nombre</label>
        <input
          type="text"
          v-model="form.nombre_contacto"
          id="nombre"
          required
        />
      </div>

      <div class="form-group">
        <label for="apellido">Id</label>
        <input
          type="text"
          v-model="form.solicitante_id"
          id="apellido"
          required
        />
      </div>

      <div class="form-group">
        <label for="telefono">Teléfono</label>
        <input type="tel" v-model="form.telefono" id="telefono" required />
      </div>

      <div class="form-group">
        <label for="documento">Número de documento</label>
        <input type="text" v-model="form.documento" id="documento" required />
      </div>

      <button type="submit">Enviar</button>
    </form>
  </div>
</template>

<script>
import axios from "axios"; // Importa axios

export default {
  data() {
    return {
      URL_API:
        "https://debidadiligencia.saitempsa.com:8484/aplicaciones/api/public/",
      form: {
        nombre_contacto: "",
        solicitante_id: "",
        telefono: "",
        correo: "",
      },
    };
  },
  methods: {
    urlExterna() {
      const urlCompleta = window.location.href;
      if (urlCompleta.includes("debidadiligencia.saitempsa.com")) {
        this.URL_API =
          "https://debidadiligencia.saitempsa.com:8484/aplicaciones/api/public/";
      }
    },
    configHeader() {
      let config = {
        headers: {
          Authorization: "Bearer " + localStorage.getItem("access_token"),
        },
      };
      return config;
    },
    submitForm() {
      let config = this.configHeader();
      const url = `${this.URL_API}api/v1/seguimientocrm`; // Corrige el uso de this
      console.log(this.form);
      axios
        .post(url, this.form, config) // Corrige el acceso al objeto form
        .then((response) => {
          console.log(response.data);
          alert("Formulario enviado con éxito");
        })
        .catch((error) => {
          console.error("Error al enviar el formulario", error);
          alert("Hubo un error al enviar el formulario");
        });
    },
  },
};
</script>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}

h2 {
  text-align: center;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 8px;
  box-sizing: border-box;
}

button {
  width: 100%;
  padding: 10px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #45a049;
}
</style>
