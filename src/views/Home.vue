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
    </div>

  </div>
</template>

<script>
  import {getAuthenticationToken} from '@/dataStorage';

  export default{
    name: "Home",
    beforeCreate( ){
      if( !getAuthenticationToken( ) ){
        this.$router.push( {name: 'login'} )
      }
    }
  }
</script>

<style>

</style>
