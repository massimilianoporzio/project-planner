<template>
  <Navbar/>
  <router-view/>
</template>

<style>
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  /*text-align: center;*/
  color: #555;
}

</style>

<script setup>
import Navbar from "@/components/Navbar";

</script>
