<template>
  <div class="container-fluid mt-2">
    <h1>Laboratorio 2</h1>
    <div class="row ">
    <router-link
    class="btn btn-primary m-2"
    to="/mis-cursos"
    >
      Mis cursos
    </router-link>
    <router-link
    class="btn btn-success m-2"
    to="/principal/roles"
    >
      Roles  
    </router-link>
    <router-link
    class="btn btn-warning m-2"
    to="/principal/nuevo-rol"
    >
      Nuevo Rol  
    </router-link>
    </div>
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
