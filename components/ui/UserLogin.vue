<template>
  <v-card rounded color="#EC9143" class="pa-7">
    <v-card-title>
      <v-row class="rowCard fontTitle">
        Welcome
      </v-row>
      <v-row class="rowCard fontTitle">
        Back
      </v-row>
    </v-card-title>
    <v-card-text>
      <v-row>
        <v-text-field v-model="email" rounded label="E-Mail" outlined />
      </v-row>
      <v-row>
        <v-text-field v-model="password" rounded label="E-password" outlined type="password" />
      </v-row>
    </v-card-text>
    <v-card-actions>
      <v-col cols="12">
        <v-row class="rowCard">
          <v-btn block class="pa-2" color="#134700" @click="login">
            <span style="text-transform: none; color: white;">Log-in</span>
          </v-btn>
        </v-row>
        <v-row class="rowCard">
          <span> If you didn't have account</span>
          <a href="">Sign-Up</a>
        </v-row>
      </v-col>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  data () {
    return {
      email: null,
      password: null
    }
  },
  methods: {
    async login () {
      await console.log('@@@ datos => ', this.email, this.password)
      const sendData = {
        email: this.email,
        password: this.password
      }
      await this.$auth.loginWith('local', {
        data: sendData
      }).then(async (res) => {
        const result = await res.data
        if (result.message === 'success') {
          this.$store.commit('setToken', result.token)
          this.$router.push('/dashboard')
        }
      }).catch((err) => {
        console.log('@@@ error => ', err)
      })
    }
  }
}
</script>

<style scoped>
.rowCard {
  width: 100%;
  display: flex;
  justify-content: center;
}
.fontTitle {
  font-size: 52px!important;
  line-height: 78px!important;
}
</style>
