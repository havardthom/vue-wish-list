<template>
  <v-app>
    <Snow color="#ffffff"/>
    <v-app-bar
      app
      style="background: linear-gradient(to right, #aa3a38, #2f7336 )"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://www.freeiconspng.com/uploads/christmas-tree-icon-15.png"
          transition="scale-transition"
          width="60"
        />
        <v-toolbar-title>GBS Technical Meetup</v-toolbar-title>
      </div>
      

      <v-spacer></v-spacer>
      <v-btn text to="/">Home</v-btn>
      <v-btn text to="/about">About</v-btn>
      <v-btn text to="/wish-list">Wish List</v-btn>
      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <router-view />
    </v-content>
  </v-app>
</template>

<script>

import Snow from 'vue-niege'

export default {
  name: 'App',
  components: { Snow },
  data: () => ({
    //
  }),
  created () {
    this.$vuetify.theme.dark = true
  }
};
</script>
