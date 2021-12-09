<template>
  <div class="col-12 text-center">
    <h2 class="text-primary"><b>Mis Roles</b></h2>
    <br>
    <div v-for="role in roles" :key="role.id">
      <h3>{{ role.roleName }}</h3>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import {getAuthenticationToken} from '@/dataStorage';

const requestPath = '/mis-roles';

export default {
  name: 'Roles',
  data( ){
    return {
      roles: [{id: 1, roleName: 'My Role'}]
    }
  },
  beforeCreate(){
    axios.get( this.$store.state.backURL + requestPath, { params: { access_token: getAuthenticationToken( ) } } )
        .then( response => {
          if( response.status !== 200 ){
            alert( 'Error Obteniendo sus roles' );
          }else{
            this.roles = response.data;
          }
        } ).catch( error => {
          alert( 'Error en la petición' );
          console.log( error );
        } );
  }
}
</script>

<style scoped>

</style>
