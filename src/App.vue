<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheTable from './components/TheTable.vue'
</script>

<template>
  
  
  <header>
    <nav class="navbar fixed-top navbar-dark bg-primary">
      <a class="navbar-brand" href="#"> <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="75" height="75" /> Just a list </a>
      
    </nav>
    <div class="wrapper">
      <HelloWorld msg="List of Mfr" />
    </div>
  </header>
  <main>
    <TheTable/> <!--the Table-->
  </main>
</template>

<script>
</script>

<style scoped>
.navbar-brand {
  margin-left: 40px;
}
.wrapper{
  margin-top: 100px;
}
</style>
