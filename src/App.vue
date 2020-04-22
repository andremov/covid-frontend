<template>
  <v-app>
    <Mapa />
    <router-view />
  </v-app>
</template>

<script>
import Mapa from "./components/Mapa";

export default {
  name: "App",

  components: {
    Mapa
  },

  data: () => ({
    //
  }),
  created: function () {
    this.$http.interceptors.response.use(undefined, function (err) {
      return new Promise(function (resolve, reject) {
        if (err.status === 401 && err.config && !err.config.__isRetryRequest) {
          this.$store.dispatch(logout)
        }
        throw err;
      });
    });
  }
};
</script>
