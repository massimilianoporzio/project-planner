<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input type="text" required v-model="title">
    <label>Details:</label>
    <textarea required v-model="details"></textarea>
    <button>Update Project</button>
  </form>

</template>

<script setup>

const  name = "EditProject"
import {onMounted, ref} from "vue";
import {useRouter} from "vue-router";
const props = defineProps(['id'])
const uri = "http://localhost:3000/projects/" + props.id
let title = ref('')
let details = ref('')
const router = useRouter()

onMounted(()=>{
  fetch(uri)
  .then(res=>res.json()).then(data=>{
    title.value=data.title
    details.value=data.details
  })
})

function handleSubmit(){
  fetch(uri,{
    method: 'PATCH',
    headers: {'Content-Type':'application/json'},
    body:JSON.stringify({
      title: title.value,
      details: details.value
    })
  }).then(()=>{
    router.push('/')
  }).catch(err=>console.log(err))
}


</script>

<style scoped>

</style>
