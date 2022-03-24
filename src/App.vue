<template>
  <v-app>
    <v-app-bar app>
      <b class="mr-2">Alesandro Žužić </b> - <u class="ml-2"> Web Aplikacije - Zadatak [2]</u>

      <v-spacer></v-spacer>

      <v-switch
        v-model="$vuetify.theme.dark"
        hide-details
        label="Tamna tema"
      ></v-switch>
    </v-app-bar>
    
    <router-view/>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  async created() {
    this.$vuetify.theme.dark = true;
  }
};
</script>

