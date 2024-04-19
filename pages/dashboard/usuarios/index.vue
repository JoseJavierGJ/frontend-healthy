<template>
  <v-col cols="12">
    <v-row>
      <v-btn block color="#123CCC" @click="showDialog = true">
        <span style="text-transform: none; color: white">
          Usuario Nuevo
        </span>
      </v-btn>
    </v-row>
    <v-row>
      <v-data-table
        :headers="headers"
        :items="usuarios"
      />
    </v-row>
    <v-dialog
      v-model="showDialog"
      persistent
      width="500"
      transition="dialog-bottom-transition"
    >
      <v-card>
        <v-card-title>Agregar Usuarios</v-card-title>
        <v-card-text>
          <v-row width="100%">
            <v-text-field
              v-model="email"
              class="pa-2 ma-2"
              label="Correo"
              placeholder="Escribre tu Password"
              outlined
            />
          </v-row>
          <v-row width="100%">
            <v-text-field
              v-model="password"
              class="pa-2 ma-2"
              label="Password"
              placeholder="Escribre tu Password"
              outlined
              type="password"
            />
          </v-row>
        </v-card-text>
        <v-card-actions>
          <v-col cols="6">
            <v-btn block color="green" @click="registrarUsuario">
              <span style="text-transform: none; color: white;">
                Registrar
              </span>
            </v-btn>
          </v-col>
          <v-col cols="6">
            <v-btn block color="red" @click="showDialog = false">
              <span style="text-transform: none; color: white;">
                Cancelar
              </span>
            </v-btn>
          </v-col>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-col>
</template>

<script>
import { mapState } from 'vuex'
export default {
  layout: 'dashboard',
  auth: true,
  data () {
    return {
      usuarios: [],
      headers: [
        {
          text: 'Email',
          value: 'email',
          align: 'center',
          sortable: true
        },
        {
          text: 'Password',
          value: 'password',
          align: 'center',
          sortable: true
        }
      ],
      showDialog: false,
      email: null,
      password: null
    }
  },
  computed: {
    ...mapState({
      token: state => state.token
    })
  },
  mounted () {
    this.obtenerUsuarios()
  },
  methods: {
    obtenerUsuarios () {
      const url = '/get-all-users'
      this.$axios.get(url)
        .then((res) => {
          console.log('response => ', res)
          if (res.data.message === 'success') {
            this.usuarios = res.data.users
          }
        })
        .catch((error) => {
          console.log('error => ', error)
        })
    },
    registrarUsuario () {
      const url = '/register'
      const data = {
        email: this.email,
        password: this.password
      }
      this.$axios.post(url, data)
        .then((res) => {
          console.log('@@ res =>', res)
          if (res.data.message === 'User registered successfully') {
            this.showDialog = false
          }
          this.obtenerUsuarios()
        })
        .catch((error) => {
          console.log('@@ error => ', error)
        })
    }
  }
}
</script>
