<template>
<div class="project" :class="{complete: project.complete}">
  <div class="actions">
    <h3 @click="showDetails=!showDetails">{{project.title}} </h3>
    <div class="icons">
      <router-link :to="{name: 'EditProject',params:{id: project.id}}">
        <span class="material-icons">edit</span>
      </router-link>

      <span @click="deleteProject" class="material-icons">delete</span>
      <span @click="toggleComplete" class="material-icons" :class="project.complete? 'tick' : ''">done</span>

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
const uri = "http://localhost:3000/projects/" + props.project.id

let showDetails = ref(false)
const props = defineProps({
  project: {
    type: Object,
    required: true
   }
  }
)

const emits = defineEmits(['delete','complete'])

function toggleComplete(){
  fetch(uri,
      {
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({complete: !props.project.complete})
            }).then(()=>{
              emits('complete',props.project.id)
          }).catch(err=>console.log(err))

}

function deleteProject(projectId){
  fetch(uri,{method: 'DELETE'})
  .then(()=>{emits('delete', props.project.id)})
  .catch(err => console.log(err))
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
.project.complete {
  border-left: 4px solid #00ce89;

}

.project.complete .tick {
  color: #00ce89;
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
