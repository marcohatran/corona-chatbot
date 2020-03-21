<template>
  <v-app>
    <v-app-bar
      app
      color="rgb(39, 116, 255)"
      dark
    >
      <div class="d-flex align-center">
       <v-icon size="50">mdi-robot</v-icon>

       <h2 class="pt-2 ml-5"> Corona Chatbot</h2>
      </div>

      <v-spacer></v-spacer>
      <v-btn
              href="https://github.com/vuetifyjs/vuetify/releases/latest"
              text
      >
        <span style="text-transform: initial">What is COVID-19 ?</span>
      </v-btn>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        text
      >
        <span style="text-transform: initial">About </span>
      </v-btn>

    </v-app-bar>

    <v-content>
      <router-view></router-view>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',

  components: {
    HelloWorld,
  },

  data: () => ({
    //
  }),
};
</script>
