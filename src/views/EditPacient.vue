<template>
  <div>
      <Header />
      <div class="container mt-4">
          <div class="row">
              <div class="col-md-12 col-sm-12 col-lg-12 col-xl-12">
                  <div class="card shadow-lg">
                      <div class="card-header">Editar paciente</div>

                      <div class="card-body">
                          <form>
                              <div class="row">
                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Codigo Postal: </label>
                                        <input type="text" class="form-control" v-model="editForm.codigoPostal">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Correo: </label>
                                        <input type="email" class="form-control" v-model="editForm.correo">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Dni: </label>
                                        <input type="text" class="form-control" v-model="editForm.dni">
                                    </div>
                                </div>
                              </div>

                              <div class="row">
                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Fecha de nacimiento: </label>
                                        <input type="date" class="form-control" v-model="editForm.fechaNacimiento">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Genero: </label>
                                        <input type="text" class="form-control" v-model="editForm.genero">
                                    </div>
                                </div>

                                <div class="col-md-4 col-sm-12 col-lg-4 col-xl-4">
                                    <div class="form-group">
                                        <label>Teléfono: </label>
                                        <input type="text" class="form-control" v-model="editForm.telefono">
                                    </div>
                                </div>
                              </div>

                              <div class="col-md-12 col-sm-12 col-lg-12 col-xl-12">
                                  <div class="form-group">
                                      <label>Direccion: </label>
                                      <input type="text" class="form-control" v-model="editForm.direccion">
                                  </div>
                              </div>

                              <div class="d-grid gap-2 mt-4">
                                  <button class="btn btn-primary" @click.prevent="onEdit()">
                                      Editar
                                  </button>
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
import Header from '@/components/Header.vue'

export default {
    name: 'EditPacient',
    components: {   
        Header
    },

    mounted() {
        this.editForm.pacientId = this.$route.params.id;

        console.log(this.pacientId)
        this.editPacient()
    },

    data() {
        return {
            editForm: {
                pacientId: '',
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
        editPacient() {
            axios.get('https://api.solodata.es/pacientes?id=' + this.editForm.pacientId)
                .then(response => {
                    console.log(response)

                    this.editForm.nombre = response.data[0].Nombre;
                    this.editForm.direccion = response.data[0].Direccion;
                    this.editForm.dni = response.data[0].DNI;
                    this.editForm.correo = response.data[0].Correo;
                    this.editForm.codigoPostal = response.data[0].CodigoPostal;
                    this.editForm.genero = response.data[0].Genero;
                    this.editForm.telefono = response.data[0].Telefono;
                    this.editForm.fechaNacimiento = response.data[0].FechaNacimiento;

                    this.editForm.token = localStorage.getItem('token')
                    console.log(this.editForm)
                })
                .catch(error => {
                    console.error(error)
                })
        },

        onEdit() {
            axios.put('https://api.solodata.es/pacientes', this.editForm)
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