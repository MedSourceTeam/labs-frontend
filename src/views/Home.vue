<template>
  <div class="container-fluid mt-2">
    <h1>Bienvenido al dummy</h1>
    <div class="row">
      <router-view></router-view>
      <div v-if="isTeacher">Soy profesor</div>
    </div>
  </div>
</template>

<script>
import { getAuthenticationToken } from "@/dataStorage";
import axios from "axios";

export default {
  name: "Home",

  data: function() {
    return {
      isTeacher: false,
    };
  },

  beforeCreate() {
    if (!getAuthenticationToken()) {
      this.$router.push({ name: "login" });
    }

    axios
      .get(this.$store.state.backURL + "/mis-roles", {
        params: { access_token: getAuthenticationToken() },
      })
      .then((response) => {
        if (response.status !== 200) {
          alert("Error Obteniendo sus roles");
        } else {
          for (let r of response.data) {
            if (r.id === 2) {
              this.isTeacher = true;
              break;
            }
          }
        }
      })
      .catch((error) => {
        alert("Error en la petición");
        console.log(error);
      });
  },
};
</script>

<style></style>
