<template>
  <v-row>
    AQUI VA LA TABLA
  </v-row>
</template>

<script>
import { mapState } from 'vuex'
export default {
  layout: 'dashboard',
  auth: true,
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
      const url = process.nextTick.URL_BASE + '/get-all-users'
      const config = {
        headers: {
          Authorization: `Bearer ${this.token}`
        }
      }
      this.$axios.get(url, config)
        .then((res) => {
          console.log('response => ', res)
        })
        .catch((error) => {
          console.log('error => ', error)
        })
    }
  }
}
</script>
