<template>
  <v-app>
    <v-main>
      <v-sheet
        class="pa-0 ma-0"
        height="100vh"
        width="100vw"
        color="#FFDEC8"
      >
        <v-row>
          <v-col cols="6">
            <v-row height="300px" align="center" justify="center">
              <h1>Clinic Patient's Dashboard</h1>
            </v-row>
            <v-row align="center" justify="center">
              <v-img :src="require('@/assets/images/logo.svg')" />
            </v-row>
          </v-col>
          <v-col cols="6" style="height: 100%!important;" align-self="center">
            <Nuxt />
          </v-col>
        </v-row>
      </v-sheet>
    </v-main>
  </v-app>
</template>
