<template>
  <div class="container">
    <Loading :loading="loading" />
    <div class="row">
      <div class="col-2">
        <img style="width: 80%" src="../assets/logo1.png" alt="" />
      </div>

      <div class="col-4 versionamiento" :style="'font-size:' + 'rem'">
        <div class="row">
          <p>FR-GCA-04</p>
          <p>Version 1</p>
          <p>30-09-2024</p>
        </div>
      </div>
    </div>
    <h2>Registro de datos personales</h2>

    <div id="seccion">
      <form @submit.prevent="submitForm" class="row g-3">
        <div class="row">
          <div class="col">
            <h5>1. Información personal</h5>
          </div>
          <div class="col">
            <SearchInput @search="handleSearch" />
          </div>
        </div>

        <div class="info_container">
          <div class="row mb-4">
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="nombre">Primer nombre:*</label>
              <input class="form-control" type="text" v-model="form.nom1_emp" id="nombre" required />
            </div>
            <div class="col-12 col-lg-6">
              <label class="form-label" for="nombre2">Segundo nombre:</label>
              <input class="form-control" type="text" v-model="form.nom2_emp" id="nombre2" />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="apellido">Primer apellido:*</label>
              <input class="form-control" type="text" v-model="form.ap1_emp" id="apellido" required />
            </div>
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="apellido2">Segundo Apellido:*</label>
              <input class="form-control" type="text" v-model="form.ap2_emp" id="apellido2" required />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Tipo de documento:*" @selectTipoId="selectTipoId" eventoCampo="selectTipoId"
                nombreItem="des_tip" :consulta="nom_tip_doc" :registros="consulta_tipo_id"
                placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 mt-2 was-validated p-2 col-lg-6">
              <div>
                <label class="form-label" for="documento">Número de documento:*</label>
                <input class="form-control" type="number" v-model="form.cod_emp" id="documento"
                  :disabled="form.tip_ide == '' || form.emp_id ? true : false" required />
                <div class="invalid-feedback errorCheck">
                  {{ "" }}
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Pais de expedicion:*" @getPaises="getPaises" eventoCampo="getPaises"
                nombreItem="nom_pai" :consulta="pai_exp_name" :registros="paises" :index="1"
                placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Departamento de expedicion:*" @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento" nombreItem="nom_dep" :consulta="dep_exp_name"
                :registros="consulta_departamentos[1]" :index="1" :disabled="!form.pai_exp"
                placeholder="Seleccione una opción" />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Ciudad de expedicion:*" @selectCiudad="selectCiudad" eventoCampo="selectCiudad"
                nombreItem="nom_ciu" :consulta="ciu_exp_name" :registros="consulta_ciudades[1]" :index="1"
                :disabled="!form.dpt_exp" placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Pais de nacimiento:*" @getPaises="getPaises" eventoCampo="getPaises"
                nombreItem="nom_pai" :consulta="cod_pai_name" :registros="paises" :index="2"
                placeholder="Seleccione una opción" />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Departamento de nacimiento:*" @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento" nombreItem="nom_dep" :consulta="cod_dep_name"
                :registros="consulta_departamentos[2]" :index="2" :disabled="!form.cod_pai"
                placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Ciudad de nacimiento:*" @selectCiudad="selectCiudad" eventoCampo="selectCiudad"
                nombreItem="nom_ciu" :consulta="cod_ciu_name" :registros="consulta_ciudades[2]" :index="2"
                :disabled="!form.cod_dep" placeholder="Seleccione una opción" />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="fecha_nac">Fecha de nacimiento:*</label>
              <input class="form-control" type="date" v-model="form.fec_nac" id="fecha_nac" required />
            </div>
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="direccion">Direccion residencia:*</label>
              <input class="form-control" type="text" v-model="form.dir_res" id="direccion" required />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="fecha_exp">Fecha expedicion:*</label>
              <input class="form-control" type="date" v-model="form.fec_expdoc" id="fecha_exp" required />
            </div>
            <div class="col-12 col-lg-6">
              <label class="form-label" for="fijo">Teléfono fijo:</label>
              <input class="form-control" type="text" v-model="form.tel_res" id="fijo" maxlength="7" />
            </div>
          </div>
          <div class="row mb-4">
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="celular">Teléfono celular:*</label>
              <input class="form-control" type="text" v-model="form.tel_cel" id="celular" required maxlength="10" />
            </div>
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="email">Correo electronico:*</label>
              <input class="form-control" type="text" v-model="form.e_mail" id="email" required />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Pais de residencia:*" @getPaises="getPaises" eventoCampo="getPaises"
                nombreItem="nom_pai" :consulta="pai_res_name" :index="3" :registros="paises"
                placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Departamento de residencia:*" @selectDepartamento="selectDepartamento"
                eventoCampo="selectDepartamento" nombreItem="nom_dep" :consulta="dep_res_name"
                :registros="consulta_departamentos[3]" :index="3" :disabled="!form.pai_res"
                placeholder="Seleccione una opción" />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Ciudad de residencia:*" @selectCiudad="selectCiudad" eventoCampo="selectCiudad"
                nombreItem="nom_ciu" :consulta="ciu_res_name" :registros="consulta_ciudades[3]" :index="3"
                :disabled="!form.dpt_res" placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Banco:*" @selectBanco="selectBanco" eventoCampo="selectBanco"
                nombreItem="nom_ban" :consulta="banco_name" :registros="consulta_banco"
                placeholder="Seleccione una opción" />
            </div>
          </div>

          <div class="row mb-4">
            <div class="col-12 col-lg-6">
              <label class="form-label" for="cuenta">Número de cuenta:</label>
              <input class="form-control" type="number" v-model="form.cta_ban" id="cuenta" :disabled="form.cod_ban == '' || form.cod_ban == 0 ? true : false
                " required />
            </div>
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="barrio">Barrio:*</label>
              <input class="form-control" type="text" v-model="form.barrio" id="barrio" required />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Nivel académico:*" @selectAcademico="selectAcademico"
                eventoCampo="selectAcademico" nombreItem="des_est" :consulta="niv_aca_name"
                :registros="consulta_estudio" placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 mt-2 was-validated p-2 col-lg-6">
              <label class="form-label" for="genero">Identidad de género:*</label>
              <select class="form-select" name="" id="genero" v-model="form.sex_emp" required>
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
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="personas_cargo">Personas a cargo(cantidad):*</label>
              <input class="form-control" type="text" v-model="form.per_car" id="personas_cargo" required />
            </div>
            <div class="col-12 was-validated col-lg-6">
              <label class="form-label" for="sangre">Grupo sanguíneo:*</label>
              <select class="form-select" name="" id="sangre" v-model="form.gru_san" required>
                <option value="A">A</option>
                <option value="AB">AB</option>
                <option value="B">B</option>
                <option value="O">O</option>
              </select>
            </div>
          </div>
          <div class="row">
            <div class="col-12 mt-2 was-validated p-2 col-lg-6">
              <label class="form-label" for="rh">Factor RH:*</label>
              <select name="" id="rh" class="form-select" v-model="form.fac_rhh" required>
                <option value="+">+</option>
                <option value="-">-</option>
              </select>
              <div class="invalid-feedback errorCheck">
                {{ mensaje_error }}
              </div>
            </div>
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Estado civil:*" @selectEstadoCivil="selectEstadoCivil"
                eventoCampo="selectEstadoCivil" nombreItem="des_est" :consulta="est_civ_name"
                :registros="consulta_estado_civil" placeholder="Seleccione una opción" />
            </div>
          </div>
          <div class="row">
            <div class="col-12 col-lg-6">
              <SearchList nombreCampo="Grupo étnico:*" @selectEtnia="selectEtnia" eventoCampo="selectEtnia"
                nombreItem="descripcion" :consulta="form.raza" :registros="consulta_etnia"
                placeholder="Seleccione una opción" />
            </div>
            <div class="col-12 col-lg-6 mt-2 was-validated p-2">
              <label class="form-label" for="estrato">Estrato socioeconomico:*</label>
              <select name="" id="estrato" v-model="form.est_soc" required class="form-select">
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
            <div class="info_container">
              <h6>{{ "Referencia" + " " + (index + 1) }}</h6>
              <div class="row">
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="tipo_ref">Tipo de referencia:</label>
                  <select name="" id="tipo_ref" v-model="referencia.tip_ref" required class="form-select">
                    <option value="1">Personal</option>
                    <option value="2">Familiar</option>
                  </select>
                </div>
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="parentesco">Parentesco:</label>
                  <input class="form-control" type="text" v-model="referencia.parent" id="parentesco" required />
                </div>

                <div class="col-12 col-lg-3">
                  <label class="form-label" for="fullName">Nombre completo:</label>
                  <input class="form-control" type="text" v-model="referencia.nom_ref" id="fullName" required />
                </div>
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="celular_ref">Número celular:</label>
                  <input class="form-control" type="text" v-model="referencia.cel_ref" id="celular_ref" required />
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- hijos -->
        <h5>3. Hijos</h5>
        <div class="info_container">
          <div class="row" v-for="(familiar, index) in form.familiares">
            <div class="info_container">
              <h6>{{ "Hijo" + " " + (index + 1) }}</h6>
              <div class="row">
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="">Primer apellido:</label>
                  <input class="form-control" type="text" v-model="familiar.ap1_fam" />
                </div>
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="">Segundo apellido:</label>
                  <input class="form-control" type="text" v-model="familiar.ap2_fam" id="" />
                </div>
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="">Nombre:</label>
                  <input class="form-control" type="text" v-model="familiar.nom_fam" id="" />
                </div>
                <div class="col-12 col-lg-3">
                  <label class="form-label" for="">Fecha de nacimiento:</label>
                  <input class="form-control" type="date" @input="updateFecha($event, familiar)"
                    :value="formattedDate(familiar.fec_nac)" id="" />
                </div>
              </div>
            </div>
          </div>
          <div class="row" v-if="form.familiares.length < 3">
            <div class="col-3 col-md-1 mt-3">
              <button type="button" class="btn_outline" v-on:click="addHijo">
                <i class="bi bi-plus color_green"></i>
              </button>
            </div>
          </div>
        </div>
        <h5>4. Autorización</h5>
        <div class="info_container">
          <p>
            Certifico que he comprendido el propósito, los beneficios, la
            interpretación, las limitaciones y las necesidades de que SAITEMP
            S.A. y la Empresa Usuaria para la que estoy realizando proceso de
            contratación, conozcan todos los resultados de los exámenes médicos
            practicados (ingreso, periódico, y de retiro), con el fin de
            alimentar los diferentes sistemas de vigilancia epidemiológicos. A
            su vez autorizo de manera previa, expresa e informada a SAITEMP S.A.
            para que, directamente o a través de sus empleados, asesores y/o
            terceros encargados del tratamiento de datos: (1.) realizar
            cualquier operación que tenga una finalidad lícita, tales como la
            recolección, almacenamiento, uso, circulación, supresión,
            transferencia y transmisión, sobre mis datos personales, entendidos
            como cualquier información vinculada o que pueda asociarse al
            TRABAJADOR, para el cumplimiento de los fines de SAITEMP S.A que
            incluyen pero no se limitan a: la afiliación del empleado en las
            entidades del sistema general de seguridad social y parafiscales,
            archivo y procesamiento de nómina, archivos sobre antecedentes
            disciplinarios y contractuales, reporte ante autoridades
            administrativas, laborales, fiscales, financieras o judiciales, así
            como al cumplimiento de obligaciones legales o contractuales de
            SAITEMP S.A con terceros, la debida ejecución del Contrato de
            trabajo, el cumplimiento de las políticas internas del EMPLEADOR, la
            verificación del cumplimiento de las obligaciones del TRABAJADOR, la
            administración de sus sistemas de información y comunicaciones, la
            generación de copias y archivos de seguridad de la información en
            los equipos proporcionados por SAITEMP S.A. (2.) EL TRABAJADOR
            conoce el carácter facultativo de entregar o no a SAITEMP S.A sus
            datos sensibles. (3) el TRABAJADOR reconoce que la información
            suministrada corresponde a la actualmente cuenta en las diferentes
            entidades y autoriza a SAITEMP S.A. para que pueda hacer las
            respectivas consultas y verificaciones por los diferentes medios
            (páginas web, vía telefónica, entre otros), de sus datos personales
            y/o de mi grupo familiar, incluyendo los datos de menores de edad,
            con la finalidad de que dicha información pueda ser utilizada para
            hacer las afiliaciones y trámites de contratación a su vez EL
            TRABAJADOR reconoce y acepta que el Tratamiento de sus Datos
            Personales efectuado por fuera del territorio colombiano puede
            regirse para algunos efectos por leyes extranjeras. (4.) EL
            TRABAJADOR reconoce que ha sido informado de los derechos que le
            asisten en su calidad de titular de Datos Personales, entre los que
            se encuentran los siguientes: i) conocer, actualizar y rectificar
            sus Datos Personales frente a SAITEMP S.A o quienes por cuenta de
            éste realicen el Tratamiento de sus Datos Personales; ii) solicitar
            prueba de la autorización otorgada a SAITEMP S.A salvo cuando la ley
            no lo requiera; iii) previa solicitud, ser informado sobre el uso
            que se ha dado a sus Datos Personales, por SAITEMP S.A o quienes por
            cuenta de éste realicen el Tratamiento de sus Datos Personales; iv)
            presentar ante las autoridades competente quejas por violaciones al
            régimen legal colombiano de protección de datos personales; v)
            revocar la presente autorización y/o solicitar la supresión de sus
            Datos Personales cuando la autoridad competente determine que
            SAITEMP S.A incurrió en conductas contrarias a la ley y a la
            Constitución; y vi) acceder en forma gratuita a sus Datos Personales
            que hayan sido objeto de Tratamiento. (5.) Para los fines
            estipulados en la ley, SAITEMP S.A ha designado el correo
            misdatos@saitempsa.com para la atención al TRABAJADOR en relación
            con los asuntos relativos a sus Datos Personales. SAITEMP S.A podrá
            reemplazar o designar a esta persona notificándolo por escrito a EL
            TRABAJADOR. Así mismo declaro por medio de mi firma que estoy de
            acuerdo con el proceso por el cual recibiré mis resultados médicos.
            Fui informado de las medidas que se tomará para proteger la
            confiabilidad de los resultados Médicos e información suministrada y
            garantizo que la información que suministro es veraz y confiable; y
            asumo cualquier responsabilidad por omitir datos que pueda afectar
            los procesos que se adelanten con SAITEMP S.A.
          </p>
          <h6>
            Al enviar el formulario está autorizando el tratamiento de datos*
          </h6>
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
import Loading from "./Loading.vue";

export default {
  components: {
    SearchList,
    SearchInput,
    Loading,
  },
  data() {
    return {
      loading: false,
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
      /* "https://debidadiligencia.saitempsa.com:8484/aplicaciones/api/public/", */

      form: {
        emp_id: "",
        nom1_emp: "",
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
        familiaresConsulta: [],
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
    handleSearch(cod_emp) {
      let self = this;
      axios
        .get(self.URL_API + `api/v1/recepcionEmpleado/${cod_emp}`)
        .then(function (result) {
          self.llenarFormulario(result.data.data);
        });
    },
    limpiarFromulario() {
      this.consulta_etnia = [];
      this.est_civ_name = "";
      this.consulta_estado_civil = [];
      this.niv_aca_name = "";
      this.consulta_estudio = [];
      this.banco_name = "";
      this.consulta_banco = [];
      this.consulta_tipo_id = [];
      this.nom_tip_doc = "";
      this.dep_res_name = "";
      this.dep_exp_name = "";
      this.cod_dep_name = "";
      this.paises = [];
      this.pai_exp_name = "";
      this.cod_pai_name = "";
      this.pai_res_name = "";
      this.consulta_departamentos = {};
      this.consulta_ciudades = {};
      this.ciu_exp_name = "";
      this.cod_ciu_name = "";
      this.ciu_res_name = "";
      this.form = {
        emp_id: "",
        nom1_emp: "",
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
        familiaresConsulta: [],
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
      };
    },
    addHijo() {
      if (this.form.familiares.length < 3) {
        this.form.familiares.push({
          ap1_fam: "",
          ap2_fam: "",
          nom_fam: "",
          tip_fam: 2,
          fec_nac: "",
          ocu_fam: 7,
        });
      }
    },
    llenarFormulario(item) {
      /*this.form.cod_emp = item.cod_emp;
        this.form.ap1_emp = item.ap1_emp;
        this.form.ap2_emp = item.ap2_emp;*/
      var self = this;
      this.form = item;
      this.form.cta_ban = Number(item.cta_ban);
      this.form.cod_emp = Number(item.cod_emp);
      this.form.fec_nac = this.formattedDate(item.fec_nac);
      this.form.fec_expdoc = this.formattedDate(item.fec_expdoc);
      this.nom_tip_doc = item.tipIde_nombre;
      this.pai_exp_name = item.pais_exp_nombre;
      this.cod_pai_name = item.pais_nac_nombre;
      this.pai_res_name = item.pais_res_nombre;
      this.dep_exp_name = item.dep_exp_nombre;
      this.dep_res_name = item.dep_res_nombre;
      this.cod_dep_name = item.dep_nac_nombre;
      this.ciu_exp_name = item.ciudad_exp_nombre;
      this.ciu_res_name = item.ciudad_res_nombre;
      this.cod_ciu_name = item.ciudad_nac_nombre;
      this.banco_name = item.nom_ban;
      this.est_civ_name = item.des_est;
      this.niv_aca_name = item.nivelAcademico_nombre;
      this.form.gru_san = item.gru_san.trim();
      const itemDptExp = { cod_pai: item.pai_exp };
      const itemDptNac = { cod_pai: item.cod_pai };
      const itemDptRes = { cod_pai: item.pai_res };
      const itemCiuExp = { cod_pai: item.pai_exp, cod_dep: item.dpt_exp };
      const itemCiuNac = { cod_pai: item.cod_pai, cod_dep: item.cod_dep };
      const itemCiuRes = { cod_pai: item.pai_res, cod_dep: item.dpt_res };
      this.getDepartamentos(itemDptExp, 1);
      this.getDepartamentos(itemDptNac, 2);
      this.getDepartamentos(itemDptRes, 3);
      this.getCiudades(itemCiuExp, 1);
      this.getCiudades(itemCiuNac, 2);
      this.getCiudades(itemCiuRes, 3);
      this.form.familiaresConsulta = [];
      this.form.emp_id = item.cod_emp;
      this.form.familiaresConsulta = JSON.parse(
        JSON.stringify(item.familiares)
      );
      this.form.raza = item.etnia_nombre;
    },

    formattedDate(date) {
      return date.split(" ")[0];
    },
    updateFecha(event, familiar) {
      const fecha = event.target.value;
      familiar.fec_nac = fecha;
    },
    selectEtnia(item) {
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
    showAlertConfirm(mensaje, icono) {
      this.$swal({
        position: "top",
        icon: icono,
        title: mensaje,
        showConfirmButton: false,
        timer: icono == "error" ? 3000 : 1500,
      });
    },
    showAlertQuestion(cedula) {
      return this.$swal({
        position: "top",
        title: `¿Está seguro que quiere registrar los datos con cédula ${cedula}`,
        icon: 'warning',
        showDenyButton: true,
        showCancelButton: true,
        confirmButtonText: "Guardar",
        denyButtonText: `No guardar`
      })
    },
    submitForm() {
      this.showAlertQuestion(this.form.cod_emp).then((result) => {
        if (result.isConfirmed) {
          this.loading = true;
          /*  const url = `https://debidadiligencia.saitempsa.com:8484/aplicaciones/api/public/api/v1/recepcionEmpleado`; */
          const url = `http://localhost:8080/aplicaciones/api/public/api/v1/recepcionEmpleado`;
          if (this.form.emp_id != "") {
            try {
              /*  const url = `https://debidadiligencia.saitempsa.com:8484/aplicaciones/api/public/api/v1/recepcionEmpleado/${this.form.emp_id}`; */
              const url = `http://localhost:8080/aplicaciones/api/public/api/v1/recepcionEmpleado/${this.form.emp_id}`;
              axios.put(url, this.form).then((result) => {
                this.loading = false;
                this.showAlertConfirm(result.data.message, result.data.status);
                if (result.data.status == "success") {
                  this.limpiarFromulario();
                }
                return;
              });
            } catch (error) {
              this.$showAlertConfirm("Error al actaulizar datos", "error");
              return;
            }
          } else {
            axios
              .get(this.URL_API + `api/v1/recepcionEmpleado/${this.form.cod_emp}`)
              .then((result) => {
                if (result.data.data.cod_emp) {
                  this.showAlertConfirm("Ya está registrado con este número de cédula", "error")
                  this.loading = false;
                  return
                } else {
                  axios
                    .post(url, this.form)
                    .then((response) => {
                      this.showAlertConfirm(response.data.message, response.data.status);
                      this.loading = false;
                      if (response.data.status == "success") {
                        this.limpiarFromulario();
                      }
                      return;
                    })
                }
              })

          }
        }
        else if (result.isDenied) {
          this.$swal.fire("Los cambios no fueron registrados", "", "info");
        }
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
  position: relative;
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

.btn_outline {
  background-color: #ffffff;
  border: #006b3f solid 2px;
  transition: all 0.5s ease-out;
}

.color_green {
  color: #006b3f;
}

.btn_outline:hover .color_green {
  color: #ffffff;
}

.btn_outline::after {
  content: "Agregar hijo";
  position: absolute;
  right: -160%;
  top: 50%;
  transform: translateY(-60%);
  white-space: nowrap;
  background-color: #006b3f;
  padding: 5px;
  border: 1px solid #ddd;
  opacity: 0;
  transition: all 0.5s ease-in-out;
  z-index: 10;
  height: 3em;
  border-radius: 5px;
  transform: scaleX(0%) translateY(-50%);
}

.btn_outline:hover::after {
  opacity: 1;
  transform: scaleX(100%) translateY(-50%);
}
</style>
