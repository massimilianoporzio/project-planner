<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
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

function handleDelete(id){
  projects.value = projects.value.filter(p => p.id !== id)
}

function handleComplete(id){
  let project = projects.value.find(p=>p.id===id)
  project.complete = !project.complete

}

onMounted(()=>{
  fetch("http://localhost:3000/projects")
  .then(res=>res.json())
  .then(data=>projects.value=data)
      .catch(err=>console.log(err.message))
})
</script>
