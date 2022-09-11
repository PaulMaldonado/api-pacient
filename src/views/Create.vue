<template>
  <div>
      <div class="container">
          <div class="row">
              <div class="col-md-12 col-sm-12 col-lg-12 col-xl-12">
                  <div class="card shadow-lg">
                      <div class="card-header">Crear nuevo paciente</div>

                      <div class="card-body">
                          <form @submit.prevent="newPacient()">
                              <div class="row">
                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Codigo Postal: </label>
                                        <input type="text" class="form-control" v-model="pacient.codigoPostal">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Correo: </label>
                                        <input type="email" class="form-control" v-model="pacient.correo">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Dni: </label>
                                        <input type="text" class="form-control" v-model="pacient.dni">
                                    </div>
                                </div>
                              </div>

                              <div class="row">
                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Fecha de nacimiento: </label>
                                        <input type="date" class="form-control" v-model="pacient.fechaNacimiento">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Genero: </label>
                                        <input type="text" class="form-control" v-model="pacient.genero">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Teléfono: </label>
                                        <input type="text" class="form-control" v-model="pacient.telefono">
                                    </div>
                                </div>
                              </div>

                              <div class="col-md-12 col-sm-12 col-lg-12 col-xl-12">
                                  <div class="form-group">
                                      <label>Direccion: </label>
                                      <input type="text" class="form-control" v-model="pacient.direccion">
                                  </div>
                              </div>

                              <div class="d-grid gap-2">
                                  <button class="btn btn-primary mt-4">Crear nuevo paciente</button>
                              </div>
                          </form>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
    name: 'Create',

    data() {
        return {
            pacient: {
                nombre: '',
                direccion: '',
                dni: '',
                correo: '',
                codigoPostal: '',
                genero: '',
                telefono: '',
                fechaNacimiento: '',
                token: ''
            }
        }
    },

    methods: {
        newPacient() {
            this.pacient.token = localStorage.getItem('token');

            axios.post('https://api.solodata.es/pacientes', this.pacient)
                .then(response => {
                    console.log(response)
                })
                .catch(error => {
                    console.error(error)
                })
        }
    }
}
</script>

<style scoped>

</style>