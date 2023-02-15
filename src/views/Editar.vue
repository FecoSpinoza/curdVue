<template>
    <div>
        <HeaderView />
        <div class="container">
            <form class="row g-3 needs-validation" novalidate>
              <div class="col-md-4">
                <label for="validationCustom01" class="form-label">Nombre</label>
                <input type="text" class="form-control" id="validationCustom01" v-model="form.nombre" required>
                <div class="valid-feedback">
                  Looks good!
                </div>
              </div>
              <div class="col-md-4">
                <label for="validationCustom02" class="form-label">DNI</label>
                <input type="text" class="form-control" id="validationCustom02" v-model="form.dni" required>
                <div class="valid-feedback">
                  Looks good!
                </div>
              </div>
              <div class="col-md-4">
                <label for="validationCustomUsername" class="form-label">Correo</label>
                <div class="input-group">
                  <span class="input-group-text" id="inputGroupPrepend">@</span>
                  <input type="text" class="form-control" id="validationCustomUsername" aria-describedby="inputGroupPrepend" v-model="form.correo" required>
                  <div class="invalid-feedback">
                    Please choose a username.
                  </div>
                </div>
              </div>
              <div class="col-md-6">
                <label for="validationCustom03" class="form-label">Telefono</label>
                <input type="text" class="form-control" id="validationCustom03" v-model="form.telefono" required>
                <div class="invalid-feedback">
                  Please provide a valid city.
                </div>
              </div>
              <div class="col-md-3">
                <label for="validationCustom04" class="form-label">Genero</label>
                <select class="form-select" id="validationCustom04" v-model="form.genero" required>
                  <option selected disabled value="">Choose...</option>
                  <option value="M">Masculino</option>
                  <option value="F">Femenino</option>
                </select>
                <div class="invalid-feedback">
                  Please select a valid state.
                </div>
              </div>
              <div class="col-md-3">
                <label for="validationCustom05" class="form-label">Codigo Postal</label>
                <input type="text" class="form-control" id="validationCustom05" v-model="form.codigoPostal" required>
                <div class="invalid-feedback">
                  Please provide a valid zip.
                </div>
              </div>
              <div class="col-md-3">
                <label for="validationCustom05" class="form-label">Fecha de Nacimiento</label>
                <input type="date" class="form-control" id="validationCustom05" v-model="form.fechaNacimiento" required>
                <div class="invalid-feedback">
                  Please provide a valid birthday date.
                </div>
              </div>

              <div class="col-12">
                <button class="btn btn-primary" type="button" v-on:click="editar()">Editar</button>
                <button class="btn btn-primary" type="button">Eliminar</button>
                <button class="btn btn-primary" type="button" v-on:click="salir()">Salir</button>
              </div>
            </form>
        </div>
        <FooterView />
    </div>
</template>

<script>
    import HeaderView from '@/components/Header.vue'
    import FooterView from '@/components/Footer.vue'
    import axios from 'axios';
    export default {
        name :"EditarView",
        components:{
            HeaderView,
            FooterView
        },
        data() {
            return {
                form: {
                    "pacienteId" : "",
                    "nombre" : "",
                    "dni" : "",
                    "correo":"",
                    "codigoPostal" :"",
                    "genero" : "",
                    "telefono" : "",
                    "fechaNacimiento" : "",
                    "token" : ""
                }
            }
        },
        mounted() {
            this.form.pacienteId = this.$route.params.id;
            axios.get("http://curso_apirest_YT.test/pacientes?id=" + this.form.pacienteId)
            .then( data => {
                
                this.form.nombre = data.data[0].Nombre;
                this.form.dni = data.data[0].DNI;
                this.form.correo = data.data[0].Correo;
                this.form.codigoPostal = data.data[0].CodigoPostal;
                this.form.genero = data.data[0].Genero;
                this.form.telefono = data.data[0].Telefono;
                this.form.fechaNacimiento = data.data[0].FechaNacimiento;
                this.form.token = localStorage.getItem("token");

                console.log(this.form);

            })
        },
        methods: {
            editar(){
                axios.put("http://curso_apirest_YT.test/pacientes", this.form)
                .then (data => {
                    console.log(data)
                })
            },
            salir(){
                this.$router.push("/dashboard");
            }
        },
    }
</script>

<style scoped>

</style>