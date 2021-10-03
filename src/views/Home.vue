<template>
  <div class="home">
    <FilterNav @filterChange="currentFilter=$event" :current="currentFilter"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
    <div v-else>
      <p>Loading projects...</p>
    </div>
  </div>
</template>

<script setup>
import {computed, onMounted, ref} from "vue";
import SingleProject from "@/components/SingleProject";
import FilterNav from "@/components/FilterNav";

const name = "Home"
let currentFilter = ref('all')

let projects = ref([])
let filteredProjects = computed(()=>{
  return projects.value.filter(p=>{
    if(currentFilter.value==='completed'){
      return p.complete === true
    }
    else if (currentFilter.value==='ongoing'){
      return p.complete === false
    }
    else{
      return true //all projects
    }
  })
})

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
