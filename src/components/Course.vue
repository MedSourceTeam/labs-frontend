<template>
  <div class="card m-3" style="width: 18rem;">
    <div class="card-header">
      {{enrolled.courseName}}
    </div>
    <ul class="list-group list-group-flush">
      <li class="list-group-item">{{ enrolled.courseDurationHours }}</li>
      <li class="list-group-item">{{ enrolled.role.roleName }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Course",
  props: {
    enrolled: Object
  }
}
</script>

<style scoped>

</style>
