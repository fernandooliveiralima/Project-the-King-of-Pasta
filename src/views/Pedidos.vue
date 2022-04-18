<template>
  <div class="main-container">
    <h1>manage orders</h1>
    <Dashboard/>
  </div>
</template>

<script>
import Dashboard from '../components/Dashboard.vue'

export default {
  name: 'Requests',
  components:{
    Dashboard
  }
}

</script>

<style scoped>
  h1{
    text-transform: capitalize;
  }
</style>
