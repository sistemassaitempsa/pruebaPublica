<template>
  <div class="container">
  <h2>Registro de datos</h2>
  <div id="seccion">
  <form @submit.prevent="submitForm" class="row g-3">
    <h5>1. Información personal</h5>
    <div class="info_container">
    <div class="row">
      <div class="col">
        <label class="form-label" >Primer Nombre:*</label>
        <input class="form-control"
          type="text"
          v-model="form.nom_emp"
          id="nombre"
          required
        />
      </div>
      <div class="col">
        <label class ="form-label" for="apellido">Segundo Nombre:</label class ="form-label">
        <input class="form-control"
          type="text"
          v-model="form.nom2_emp"
          id="apellido"
          required
        />
      </div>
    </div>
    <div class="row">
      <div class="col">
        <label class ="form-label" for="apellido">Primer Apellido:*</label class ="form-label">
        <input class="form-control"
          type="text"
          v-model="form.ap1_emp"
          id="apellido"
          required
        />
      </div>
      <div class="col">
        <label class ="form-label" for="apellido">Segundo Apellido:*</label class ="form-label">
        <input class="form-control"
          type="text"
          v-model="form.ap2_emp"
          id="apellido"
          required
        />
      </div>
    </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="telefono">Tipo de documento:*</label class ="form-label">
      <input class="form-control" type="tel" v-model="form.tip_ide" id="telefono" required />
    </div>

    <div class="col">
      <label class ="form-label" for="documento">Número de documento</label class ="form-label">
      <input class="form-control" type="number" v-model="form.cod_emp" id="documento" required />
    </div>
    </div>
   <div class="row">
    <div class="col">
        <SearchList
              nombreCampo="Pais de expedicion: *"
              @getPaises="getPaises"
              eventoCampo="getPaises"
              nombreItem="nom_pai"
              :consulta="form.pai_exp"
              :registros="paises"
              :ordenCampo="1"
              @getDepartamentos="getDepartamentos"
              placeholder="Seleccione una opción"
            />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Departamento de expedicion</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.dpt_exp"
        id="documento"
        required
      />
    </div>
   </div>
  <div class="row">
    <div class="col">
      <label class ="form-label" for="documento">Ciudad de expedicion</label class ="form-label">
      <input class  ="form-control"
        type="text"
        v-model="form.ciu_exp"
        id="documento"
        required
      />
    </div>
    <div class="col">
        <SearchList
              nombreCampo="Pais de nacimiento: *"
              @getPaises="getPaises"
              eventoCampo="getPaises"
              nombreItem="nom_pai"
              :consulta="form.cod_pai"
              :registros="paises"
              :ordenCampo="1"
              @getDepartamentos="getDepartamentos"
              placeholder="Seleccione una opción"
            />
    </div>
  </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Departamento de nacimiento</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.cod_dep"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Ciudad de nacimiento</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.cod_ciu"
        id="documento"
        required
      />
    </div>
    </div>
   <div class ="row">
    <div class="col">
      <label class ="form-label" for="documento">Fecha de nacimiento</label class ="form-label">
      <input class="form-control"
        type="date"
        v-model="form.fec_nac"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Direccion residencia</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.dir_res"
        id="documento"
        required
      />
    </div>
   </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Fecha expedicion</label class ="form-label">
      <input class="form-control"
        type="date"
        v-model="form.fec_expdoc"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Telefono fijo</label class ="form-label">
      <input class="form-control" type="text" v-model="form.tel_res" id="documento" required />
    </div>
    </div>
   <div class="row">
    <div class="col">
      <label class ="form-label" for="documento">Telefono celular</label class ="form-label">
      <input class="form-control" type="text" v-model="form.tel_cel" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Correo electronico</label class ="form-label">
      <input class="form-control" type="text" v-model="form.e_mail" id="documento" required />
    </div>
   </div>
   <div class="row">
    <div class="col">
        <SearchList
              nombreCampo="Pais de residencia: *"
              @getPaises="getPaises"
              eventoCampo="getPaises"
              nombreItem="nom_pai"
              :consulta="form.pai_res"
              :registros="paises"
              :ordenCampo="1"
              @getDepartamentos="getDepartamentos"
              placeholder="Seleccione una opción"
            />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Departamento de residencia</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.dpt_res"
        id="documento"
        required
      />
    </div>
   </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Ciudad de residencia</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.ciu_res"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Banco</label class ="form-label">
      <input class="form-control" type="text" v-model="form.cod_ban" id="documento" required />
    </div>
    </div>
   
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Numero de cuenta</label class ="form-label">
      <input class="form-control" type="text" v-model="form.cta_ban" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Barrio</label class ="form-label">
      <input class="form-control" type="text" v-model="form.barrio" id="documento" required />
    </div>
    </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Nivel académico</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.Niv_aca"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Identidad de género</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.sex_emp"
        id="documento"
        required
      />
    </div>
    </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Personas a cargo</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.per_car"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Grupo sanguíneo</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.gru_san"
        id="documento"
        required
      />
    </div>
    </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Factor RH</label class ="form-label">
      <input class="form-control" type="text" v-model="form.fac_rhh" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Grupo etnico</label class ="form-label">
      <input class="form-control" type="text" v-model="form.raza" id="documento" required />
    </div>
    </div>
    <div class="row">
      <div class="col">
      <label class ="form-label" for="documento">Estado civil</label class ="form-label">
      <input class="form-control" type="text" v-model="form.est_civ" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Estrato socioeconomico</label class ="form-label">
      <input class="form-control" type="text" v-model="form.est_soc" id="documento" required />
    </div>
    </div>
  </div>
    <!-- Referencias personales -->
    <!-- referencia 1 -->
    <h5>2. Referencias personales</h5>
     <div class="info_container">
<div class="row">
  <div class="col">
      <label class ="form-label" for="documento">Tipo de referencia</label class ="form-label">
      <select name="" id="" v-model="form.referencia1" required class="form-select">
        <option value="1">Personal</option>
        <option value="2">Familiar</option>
      </select>
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Parentesco</label class ="form-label">
      <input class="form-control" type="text" v-model="form.parentesco1" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Nombre completo</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.nomrbre_referencia1"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Numero de cedula</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.cedula_referencia1"
        id="documento"
        required
      />
    </div>
</div>
<div class="row">
  <div class="col">
      <label class ="form-label" for="documento">Tipo de referencia</label>
      <select name="" id="" v-model="form.referencia2" required class="form-select">
        <option value="1">Personal</option>
        <option value="2">Familiar</option>
      </select>
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Parentesco</label class ="form-label">
      <input class="form-control" type="text" v-model="form.parentesco2" id="documento" required />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Nombre completo</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.nomrbre_referencia2"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Numero de cedula</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.cedula_referencia2"
        id="documento"
        required
      />
    </div>
</div>
</div>
<h5>3. Hijos</h5>
<div class="info_container">
  <div class="row">
  <div class="col">
      <label class ="form-label" for="documento">Primer apellido</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.hijos_apellido"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Segundo apellido</label class ="form-label">
      <input class="form-control"
        type="text"
        v-model="form.hijos_apellido2"
        id="documento"
        required
      />
    </div>
    <div class="col">
      <label class ="form-label" for="documento">Nombre</label class ="form-label">
      <input class="form-control" type="text" v-model="form.hijos_nombre" id="documento" required />
    </div>
</div>
</div>

 

    <button type="submit">Enviar</button>
  </form>
</div>
</div>
</template>

<script>
import axios from "axios"; 
import SearchList from "./SearchList.vue";

export default {
  components: {
    SearchList},
  data() {
    return {
      paises:"",
      URL_API:"http://localhost:8080/aplicaciones/api/public/",
      form: {
        nom_emp:"",
        nom2_emp:"",
        cod_grupo:"",
        cod_emp:"",
        ap1_emp:"",
        ap2_emp:"",
        tip_ide:"",
        pai_exp:"",
        dpt_exp:"",
        ciu_exp:"",
        cod_pai:"",
        cod_dep:"",
        cod_ciu:"",
        fec_nac:"",
        dir_res:"",
        fec_expdoc:"",
        tel_res:"",
        tel_cel:"",
        e_mail:"",
        pai_res:"",
        dpt_res:"",
        ciu_res:"",
        cod_ban:"",
        cta_ban:"",
        barrio:"",
        Niv_aca:"",
        sex_emp:"",
        per_car:"",
        gru_san:"",
        fac_rhh:"",
        raza:"",
        est_civ:"",
        est_soc:""

      },
    };
  },
  methods: {
    getPaises() {
      if (this.paises == "") {
        let self = this;
        axios
          .get(self.URL_API + "api/v1/paisesFormularioEmpleado")
          .then(function (result) {
            self.paises = result.data;
          });
      }
    },
    submitForm() {
      const url = `http://localhost:8080/aplicaciones/api/public/api/v1/recepcionEmpleado`; // Corrige el uso de this
      console.log(this.form);
      axios
        .post(url, this.form) // Corrige el acceso al objeto form
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
h2 {
  text-align: center;
}
.col{
  margin-top: 1em;
}
.form-group {
  margin-bottom: 15px;
}
#seccion {
  border: solid #d5dbdb 0.5px;
  padding: 30px;
  margin-bottom: 30px;
  border-radius: 10px;
  box-shadow: rgba(0, 0, 0, 0.25) 0px 14px 28px,
    rgba(0, 0, 0, 0.22) 0px 10px 10px;
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
.info_container{
  border: solid rgba(214, 214, 214, 0.558) 1px;
  border-radius: 5px;
  padding: 2em
}
h5{
  color: #45a049;
}
</style>
