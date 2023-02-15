<template>
    <div>
        <HeaderView/>
        <div class="container">
            <table class="table table-hover">
                <thead>
                  <tr>
                    <th scope="col">ID</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">DNI</th>
                    <th scope="col">Telefono</th>
                    <th scope="col">Correo</th>
                  </tr>
                </thead>
                <tbody>
                  <tr v-for="paciente in listaPacientes" :key="paciente.pacienteId" v-on:click="editar(paciente.PacienteId)">
                    <th scope="row">{{paciente.PacienteId}}</th>
                    <td>{{paciente.Nombre}}</td>
                    <td>{{paciente.DNI}}</td>
                    <td>{{paciente.Telefono}}</td>
                    <td>{{paciente.Correo}}</td>
                  </tr>
                </tbody>
              </table>
        </div>
        <FooterView/>
        
    </div>
</template>

<script>
    import HeaderView from '@/components/Header.vue'
    import FooterView from '@/components/Footer.vue'
    import axios from 'axios';

    export default {
        name : "DashboardView",
        components: {
            HeaderView,
            FooterView
        },
        data() {
            return {
                listaPacientes : null,
                pagina : 1
            }
        },
        mounted(){
            let url = 'http://curso_apirest_YT.test/pacientes?page='+ this.pagina;
            axios.get(url).then( data => {
                this.listaPacientes = data.data;
            })
        },
        methods: {
            editar(id){
                this.$router.push("/editar/"+id);
            }
        },
    }
</script>

<style lang="scss" scoped>

</style>