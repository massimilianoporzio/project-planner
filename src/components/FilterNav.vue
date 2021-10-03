<template>
  <nav class="filter-nav">
    <button @click="updateFilter('all')"
            :class="{active: props.current === 'all'}"
    >View All</button>
    <button @click="updateFilter('completed')"
            :class="{active: props.current === 'completed'}"
    >Completed</button>
    <button @click="updateFilter('ongoing')"
            :class="{active: props.current === 'ongoing'}"
    >Ongoing</button>
  </nav>
</template>

<script setup>

const name = "FilterNav"
const emits = defineEmits(['filterChange'])
const props = defineProps(['current'])

function updateFilter(by){
  console.log('BY IS ',by)
 emits('filterChange',by)
}
</script>

<style scoped>
.filter-nav button {
  background: none;
  border: none;
  color: #bbb;
  outline: none;
  font-size: 12px;
  text-transform: uppercase;
  margin-right: 10px;
  letter-spacing: 1px;
  font-weight: bold;
  cursor: pointer;
}
.filter-nav button.active {
  color: #555;
}
</style>
