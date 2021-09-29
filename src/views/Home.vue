<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project"/>
      </div>
    </div>
    <div v-else>
      <p>Loading projects...</p>
    </div>
  </div>
</template>

<script setup>
import {onMounted, ref} from "vue";
import SingleProject from "@/components/SingleProject";

const name = "Home"
let projects = ref([])

onMounted(()=>{
  fetch("http://localhost:3000/projects")
  .then(res=>res.json())
  .then(data=>projects.value=data)
      .catch(err=>console.log(err.message))
})
</script>
