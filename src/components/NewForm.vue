<template>
  <div class="container">
    <h2>Registro de datos</h2>

    <div id="seccion">
      <form @submit.prevent="submitForm" class="row g-3">
        <div class="row">
          <div class="col"><h5>1. Información personal</h5></div>
          <div class="col">
            <SearchInput @search="handleSearch" />
          </div>
        </div>

        <div class="info_container">
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="nombre">Primer nombre:*</label>
              <input
                class="form-control"
                type="text"
                v-model="form.nom_emp"
                id="nombre"
                required
              />
            </div>
            <div class="col">
              <label class="form-label" for="nombre2">Segundo nombre:</label>
              <input
                class="form-control"
                type="text"
                v-model="form.nom2_emp"
                id="nombre2"
              />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="apellido">Primer apellido:*</label>
              <input
                class="form-control"
                type="text"
                v-model="form.ap1_emp"
                id="apellido"
                required
              />
            </div>
            <div class="col was-validated">
              <label class="form-label" for="apellido2"
                >Segundo Apellido:*</label
              >
              <input
                class="form-control"
                type="text"
                v-model="form.ap2_emp"
                id="apellido2"
                required
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Tipo de documento:*"
                @selectTipoId="selectTipoId"
                eventoCampo="selectTipoId"
                nombreItem="des_tip"
                :consulta="nom_tip_doc"
                :registros="consulta_tipo_id"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col mt-4 was-validated p-2">
              <div>
                <label class="form-label" for="documento"
                  >Número de documento:*</label
                >
                <input
                  class="form-control"
                  type="number"
                  v-model="form.cod_emp"
                  id="documento"
                  :disabled="form.tip_ide == '' ? true : false"
                  required
                />
                <div class="invalid-feedback errorCheck">
                  {{ "" }}
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Pais de expedicion:*"
                @getPaises="getPaises"
                eventoCampo="getPaises"
                nombreItem="nom_pai"
                :consulta="pai_exp_name"
                :registros="paises"
                :index="1"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Departamento de expedicion:*"
                @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento"
                nombreItem="nom_dep"
                :consulta="dep_exp_name"
                :registros="consulta_departamentos[1]"
                :index="1"
                :disabled="!form.pai_exp"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Ciudad de expedicion:*"
                @selectCiudad="selectCiudad"
                eventoCampo="selectCiudad"
                nombreItem="nom_ciu"
                :consulta="ciu_exp_name"
                :registros="consulta_ciudades[1]"
                :index="1"
                :disabled="!form.dpt_exp"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Pais de nacimiento:*"
                @getPaises="getPaises"
                eventoCampo="getPaises"
                nombreItem="nom_pai"
                :consulta="cod_pai_name"
                :registros="paises"
                :index="2"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Departamento de nacimiento:*"
                @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento"
                nombreItem="nom_dep"
                :consulta="cod_ciu_name"
                :registros="consulta_departamentos[2]"
                :index="2"
                :disabled="!form.cod_pai"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Ciudad de nacimiento:*"
                @selectCiudad="selectCiudad"
                eventoCampo="selectCiudad"
                nombreItem="nom_ciu"
                :consulta="cod_ciu_name"
                :registros="consulta_ciudades[2]"
                :index="2"
                :disabled="!form.cod_dep"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="fecha_nac"
                >Fecha de nacimiento:*</label
              >
              <input
                class="form-control"
                type="date"
                v-model="form.fec_nac"
                id="fecha_nac"
                required
              />
            </div>
            <div class="col was-validated">
              <label class="form-label" for="direccion"
                >Direccion residencia:*</label
              >
              <input
                class="form-control"
                type="text"
                v-model="form.dir_res"
                id="direccion"
                required
              />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="fecha_exp"
                >Fecha expedicion:*</label
              >
              <input
                class="form-control"
                type="date"
                v-model="form.fec_expdoc"
                id="fecha_exp"
                required
              />
            </div>
            <div class="col">
              <label class="form-label" for="fijo">Telefono fijo:</label>
              <input
                class="form-control"
                type="text"
                v-model="form.tel_res"
                id="fijo"
              />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="celular">Telefono celular:*</label>
              <input
                class="form-control"
                type="text"
                v-model="form.tel_cel"
                id="celular"
                required
              />
            </div>
            <div class="col was-validated">
              <label class="form-label" for="email">Correo electronico:*</label>
              <input
                class="form-control"
                type="text"
                v-model="form.e_mail"
                id="email"
                required
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Pais de residencia:*"
                @getPaises="getPaises"
                eventoCampo="getPaises"
                nombreItem="nom_pai"
                :consulta="pai_res_name"
                :index="3"
                :registros="paises"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Departamento de residencia:*"
                @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento"
                nombreItem="nom_dep"
                :consulta="dep_res_name"
                :registros="consulta_departamentos[3]"
                :index="3"
                :disabled="!form.pai_res"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Ciudad de residencia:*"
                @selectCiudad="selectCiudad"
                eventoCampo="selectCiudad"
                nombreItem="nom_ciu"
                :consulta="ciu_res_name"
                :registros="consulta_ciudades[3]"
                :index="3"
                :disabled="!form.dpt_res"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Banco:*"
                @selectBanco="selectBanco"
                eventoCampo="selectBanco"
                nombreItem="nom_ban"
                :consulta="banco_name"
                :registros="consulta_banco"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>

          <div class="row mb-4">
            <div class="col">
              <label class="form-label" for="cuenta">Número de cuenta:</label>
              <input
                class="form-control"
                type="number"
                v-model="form.cta_ban"
                id="cuenta"
                :disabled="
                  form.cod_ban == '' || form.cod_ban == 0 ? true : false
                "
                required
              />
            </div>
            <div class="col was-validated">
              <label class="form-label" for="barrio">Barrio:*</label>
              <input
                class="form-control"
                type="text"
                v-model="form.barrio"
                id="barrio"
                required
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Nivel académico:*"
                @selectAcademico="selectAcademico"
                eventoCampo="selectAcademico"
                nombreItem="des_est"
                :consulta="niv_aca_name"
                :registros="consulta_estudio"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col mt-4 was-validated p-2">
              <label class="form-label" for="genero"
                >Identidad de género:*</label
              >
              <select
                class="form-select"
                name=""
                id="genero"
                v-model="form.sex_emp"
                required
              >
                <option value="1">Mujer</option>
                <option value="2">Hombre</option>
                <option value="0">Otro</option>
              </select>
              <div class="invalid-feedback errorCheck">
                {{ "" }}
              </div>
            </div>
          </div>
          <div class="row mb-4">
            <div class="col was-validated">
              <label class="form-label" for="personas_cargo"
                >Personas a cargo(cantidad):*</label
              >
              <input
                class="form-control"
                type="text"
                v-model="form.per_car"
                id="personas_cargo"
                required
              />
            </div>
            <div class="col was-validated">
              <label class="form-label" for="sangre">Grupo sanguíneo:*</label>
              <select
                class="form-select"
                name=""
                id="sangre"
                v-model="form.gru_san"
                required
              >
                <option value="A">A</option>
                <option value="AB">AB</option>
                <option value="B">B</option>
                <option value="O">O</option>
              </select>
            </div>
          </div>
          <div class="row">
            <div class="col mt-4 was-validated p-2">
              <label class="form-label" for="rh">Factor RH:*</label>
              <select
                name=""
                id="rh"
                class="form-select"
                v-model="form.fac_rhh"
                required
              >
                <option value="+">+</option>
                <option value="-">-</option>
              </select>
              <div class="invalid-feedback errorCheck">
                {{ mensaje_error }}
              </div>
            </div>
            <div class="col">
              <SearchList
                nombreCampo="Estado civil:*"
                @selectEstadoCivil="selectEstadoCivil"
                eventoCampo="selectEstadoCivil"
                nombreItem="des_est"
                :consulta="est_civ_name"
                :registros="consulta_estado_civil"
                placeholder="Seleccione una opción"
              />
            </div>
          </div>
          <div class="row">
            <div class="col">
              <SearchList
                nombreCampo="Grupo étnico:*"
                @selectEtnia="selectEtnia"
                eventoCampo="selectEtnia"
                nombreItem="descripcion"
                :consulta="form.raza"
                :registros="consulta_etnia"
                placeholder="Seleccione una opción"
              />
            </div>
            <div class="col mt-4 was-validated p-2">
              <label class="form-label" for="estrato"
                >Estrato socioeconomico:*</label
              >
              <select
                name=""
                id="estrato"
                v-model="form.est_soc"
                required
                class="form-select"
              >
                <option :value="n" :key="n" v-for="n in 6">{{ n }}</option>
              </select>
              <div class="invalid-feedback errorCheck">
                {{ mensaje_error }}
              </div>
            </div>
          </div>
        </div>
        <!-- Referencias personales -->
        <!-- referencia 1 -->
        <h5>2. Referencias personales</h5>
        <div class="info_container">
          <div class="row" v-for="(referencia, index) in form.referencias">
            <div class="col">
              <label class="form-label" for="tipo_ref"
                >Tipo de referencia:</label
              >
              <select
                name=""
                id="tipo_ref"
                v-model="referencia.tip_ref"
                required
                class="form-select"
              >
                <option value="1">Personal</option>
                <option value="2">Familiar</option>
              </select>
            </div>
            <div class="col">
              <label class="form-label" for="parentesco">Parentesco:</label>
              <input
                class="form-control"
                type="text"
                v-model="referencia.parent"
                id="parentesco"
                required
              />
            </div>
            <div class="col">
              <label class="form-label" for="fullName">Nombre completo:</label>
              <input
                class="form-control"
                type="text"
                v-model="referencia.nom_ref"
                id="fullName"
                required
              />
            </div>
            <div class="col">
              <label class="form-label" for="celular_ref"
                >Número celular:</label
              >
              <input
                class="form-control"
                type="text"
                v-model="referencia.cel_ref"
                id="celular_ref"
                required
              />
            </div>
          </div>
        </div>

        <!-- hijos -->
        <h5>3. Hijos</h5>
        <div class="info_container">
          <div class="row" v-for="(familiar, index) in form.familiares">
            <div class="col">
              <label class="form-label" for="">Primer apellido:</label>
              <input
                class="form-control"
                type="text"
                v-model="familiar.ap1_fam"
              />
            </div>
            <div class="col">
              <label class="form-label" for="">Segundo apellido:</label>
              <input
                class="form-control"
                type="text"
                v-model="familiar.ap2_fam"
                id=""
              />
            </div>
            <div class="col">
              <label class="form-label" for="">Nombre:</label>
              <input
                class="form-control"
                type="text"
                v-model="familiar.nom_fam"
                id=""
              />
            </div>
            <div class="col">
              <label class="form-label" for="">Fecha de nacimiento:</label>
              <input
                class="form-control"
                type="date"
                v-model="familiar.fec_nac"
                id=""
              />
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
import SearchInput from "./SearchInput.vue";

export default {
  components: {
    SearchList,
    SearchInput,
  },
  data() {
    return {
      mensaje_error: "¡Este campo debe ser diligrenciado!",
      consulta_etnia: [],
      est_civ_name: "",
      consulta_estado_civil: [],
      niv_aca_name: "",
      consulta_estudio: [],
      banco_name: "",
      consulta_banco: [],
      consulta_tipo_id: [],
      nom_tip_doc: "",
      dep_res_name: "",
      dep_exp_name: "",
      cod_dep_name: "",
      paises: [],
      pai_exp_name: "",
      cod_pai_name: "",
      pai_res_name: "",
      consulta_departamentos: {},
      consulta_ciudades: {},
      ciu_exp_name: "",
      cod_ciu_name: "",
      ciu_res_name: "",
      URL_API: "http://localhost:8080/aplicaciones/api/public/",
      form: {
        nom_emp: "",
        nom2_emp: "",
        cod_grupo: "",
        cod_emp: "",
        ap1_emp: "",
        ap2_emp: "",
        tip_ide: "",
        pai_exp: "",
        dpt_exp: "",
        ciu_exp: "",
        cod_pai: "",
        cod_dep: "",
        cod_ciu: "",
        fec_nac: "",
        dir_res: "",
        fec_expdoc: "",
        tel_res: "",
        tel_cel: "",
        e_mail: "",
        pai_res: "",
        dpt_res: "",
        ciu_res: "",
        cod_ban: "",
        cta_ban: "",
        barrio: "",
        Niv_aca: "",
        sex_emp: "",
        per_car: "",
        gru_san: "",
        fac_rhh: "",
        raza: "",
        est_civ: "",
        est_soc: "",
        referencias: [
          { num_ref: 1, tip_ref: "", parent: "", cel_ref: "", nom_ref: "" },
          { num_ref: 2, tip_ref: "", parent: "", cel_ref: "", nom_ref: "" },
        ],
        familiares: [
          {
            ap1_fam: "",
            ap2_fam: "",
            nom_fam: "",
            tip_fam: 2,
            fec_nac: "",
            ocu_fam: 7,
          },
          {
            ap1_fam: "",
            ap2_fam: "",
            nom_fam: "",
            tip_fam: 2,
            fec_nac: "",
            ocu_fam: 7,
          },
          {
            ap1_fam: "",
            ap2_fam: "",
            nom_fam: "",
            tip_fam: 2,
            fec_nac: "",
            ocu_fam: 7,
          },
        ],
      },
    };
  },
  methods: {
    selectEtnia() {
      let self = this;
      axios
        .get(self.URL_API + "api/v1/grupoEtnicoEmpleado")
        .then(function (result) {
          self.consulta_etnia = result.data;
          self.form.cod_grupo = item.cod_grupo;
        });
    },
    selectEstadoCivil(item) {
      let self = this;
      axios.get(self.URL_API + "api/v1/estadocivil").then(function (result) {
        self.consulta_estado_civil = result.data;
        self.form.est_civ = item.cod_est;
      });
    },
    selectAcademico(item) {
      let self = this;
      axios
        .get(self.URL_API + "api/v1/nivelAcademicoFormEmpleado")
        .then(function (result) {
          self.consulta_estudio = result.data;
          self.form.Niv_aca = item.tip_est;
        });
    },
    selectBanco(item) {
      let self = this;
      axios
        .get(self.URL_API + "api/v1/bancosFormularioEmpleado")
        .then(function (result) {
          self.consulta_banco = result.data;
          self.form.cod_ban = item.cod_ban;
        });
    },
    selectTipoId(item) {
      let self = this;
      axios
        .get(self.URL_API + "api/v1/tipoIdFormularioEmpleado")
        .then(function (result) {
          self.consulta_tipo_id = result.data;
          self.form.tip_ide = item.cod_tip;
        });
    },
    selectCiudad(item = null, index = null) {
      if (item != null) {
        switch (index) {
          case 1:
            this.form.ciu_exp = item.cod_ciu;
            this.ciu_exp_name = item.nom_ciu;

            break;
          case 2:
            this.form.cod_ciu = item.cod_ciu;
            this.cod_ciu_name = item.nom_ciu;

            break;
          case 3:
            this.form.ciu_res = item.cod_ciu;
            this.ciu_res_name = item.nom_ciu;

            break;
        }
      }
    },
    selectDepartamento(item = null, index = null) {
      if (item != null) {
        switch (index) {
          case 1:
            this.form.dpt_exp = item.cod_dep;
            this.dep_exp_name = item.nom_dep;
            this.getCiudades(item, index);
            break;
          case 2:
            this.form.cod_dep = item.cod_dep;
            this.cod_dep_name = item.nom_dep;
            this.getCiudades(item, index);
            break;
          case 3:
            this.form.dpt_res = item.cod_dep;
            this.dep_res_name = item.nom_dep;
            this.getCiudades(item, index);
            break;
        }
      }
    },
    getCiudades(item, index) {
      let self = this;
      console.log(index);
      axios
        .get(
          self.URL_API +
            "api/v1/ciudadesFormularioEmpleado/" +
            item.cod_pai +
            "/" +
            item.cod_dep
        )
        .then(function (result) {
          self.consulta_ciudades[index] = result.data;
        });
    },
    getDepartamentos(item, index) {
      let self = this;
      console.log(index);
      axios
        .get(
          self.URL_API +
            "api/v1/departamentosFormularioEmpleado/" +
            item.cod_pai
        )
        .then(function (result) {
          self.consulta_departamentos[index] = result.data;
        });
    },
    getPaises(item = null, index = null) {
      if (item != null) {
        switch (index) {
          case 1:
            this.form.pai_exp = item.cod_pai;
            this.pai_exp_name = item.nom_pai;
            this.getDepartamentos(item, index);
            break;
          case 2:
            this.form.cod_pai = item.cod_pai;
            this.cod_pai_name = item.nom_pai;
            this.getDepartamentos(item, index);
            break;
          case 3:
            this.form.pai_res = item.cod_pai;
            this.pai_res_name = item.nom_pai;
            this.getDepartamentos(item, index);
            break;
        }
      }
      let self = this;
      axios
        .get(self.URL_API + "api/v1/paisesFormularioEmpleado")
        .then(function (result) {
          self.paises = result.data;
        });
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
.col {
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
  background-color: #006b3f;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #015734;
}
.info_container {
  border: solid rgba(214, 214, 214, 0.558) 1px;
  border-radius: 5px;
  padding: 2em;
}
h5 {
  color: #006b3f;
}
.errorCheck {
  height: 2em;
}
</style>
