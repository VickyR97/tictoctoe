<template>
  <div class="icon-outer d-flex justify-content-center align-items-center rounded">
      <i 
      v-if="iconName == 'circle'"
      class="far fa-circle fa-4x text-primary"></i>
      <i 
      v-if="iconName == 'cross'"
      class="fas fa-times fa-4x text-danger"></i>
      <i
      v-if="iconName == 'empty'"
      ></i>
  </div>
</template>

<script>
export default {
    props:{
        iconName:{
            type: String,
            required: true
        }
    }
}
</script>

<style scoped>
.icon-outer{
    height: 100px;
    width: 100px;
    background-color: white;
}
</style>