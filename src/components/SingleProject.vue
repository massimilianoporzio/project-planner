<template>
<div class="project">
  <div class="actions" @click="showDetails=!showDetails">
    <h3>{{project.title}}</h3>
    <div class="icons">
      <span class="material-icons">edit</span>
      <span @click="deleteProject(projectId)" class="material-icons">delete</span>
      <span class="material-icons">done</span>
    </div>
  </div>
  <div class="details" v-if="showDetails">
    <p>{{project.details}}</p>
  </div>
</div>
</template>

<script setup>
import {ref} from "vue";

const name = "SingleProject"
const uri = "http://localhost:3000/projects"

let showDetails = ref(false)
const props = defineProps({
  project: {
    type: Object,
    required: true
   }
  }
)
function deleteProject(projectId){

}

</script>

<style scoped>
.project {
  margin: 20px auto;
  background: white;
  padding: 10px 20px;
  border-radius: 4px;
  box-shadow: 1px 2px 3px rgba(0,0,0,0.5);
  border-left: 4px solid #e90074;
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.material-icons {
  font-size: 24px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover{
  color: #777
}
</style>
