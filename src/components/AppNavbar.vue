<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
   
   <div class="navbar-nav">
        <router-link class="nav-link" :to="{name:'Range'}">Range</router-link>
        <router-link class="nav-link" :to="{name:'Users'}">Users</router-link>
    </div>
   
  </div>
</nav>
</template>

<script>
export default {
name:'AppNavbar'
}
</script>

<style>

</style>