<template>
  <div>
    <div class="container mt-4">
        <button class="btn btn-primary" @click="create()">Nuevo paciente</button>
        <div class="row">
            <h2 class="text-center mb-4">Lista de Pacientes</h2>
            <div class="col-md-12 col-sm-12 col-lg-12 col-xl-12">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>ID</th>
                            <th>Nombre</th>
                            <th>DNI</th>
                            <th>Teléfono</th>
                            <th>Correo</th>
                            <th>Editar</th>
                            <th>Eliminar</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="pacient in listAllPacients" :key="pacient.PacienteId">
                            <th>{{ pacient.PacienteId }}</th>
                            <th>{{ pacient.Nombre }}</th>
                            <th>{{ pacient.DNI }}</th>
                            <th>{{ pacient.Telefono }}</th>
                            <th>{{ pacient.Correo }}</th>
                            <th>
                                <button class="btn btn-success" @click="edit(pacient.PacienteId)">
                                    <i class="fa-solid fa-pen-to-square"></i>
                                </button>
                            </th>
                            <th>
                                <button class="btn btn-danger" @click="remove(pacient.PacienteId)">
                                    <i class="fa-solid fa-trash"></i>
                                </button>
                            </th>
                        </tr>
                    </tbody>
                </table> 
            </div>
        </div>
    </div> 
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Table',

    data() {
        return {
            listAllPacients: [],
            page: 1,
            token: '',
        }
    },

    mounted() {
        this.listPacients()
    },

    methods: {
        listPacients() {
            const pacients = 'https://api.solodata.es/pacientes?page=' + this.page;

            axios.get(pacients)
                .then(response => {
                    console.log(response)

                    this.listAllPacients = response.data;
                })
                .catch(error => {
                    console.error(error)
                })
        },

        edit(id) {
            this.$router.push('/edit/' + id)
        },

        remove(id) {
            const token = localStorage.getItem('token')

            console.log(token)

            axios.delete('https://api.solodata.es/pacientes/' + id, {token})
                .then(response => {
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        },

        create() {
            this.$router.push('/create')
        }
    }
}
</script>

<style scoped>

</style>