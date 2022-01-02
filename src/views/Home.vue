<template>

  <div v-if="projects.length">
    <div  v-for="project in projects" :key="project.id">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SingleProject.vue'
export default {
  name: 'Home',
  components: {
    SingleProject
  },
  
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res)=>res.json())
      .then((data)=>this.projects=data)
      .catch((err)=>{console.log(err.message)})
  },

  data() {
    return{
      projects: []
    }
  },

  methods: {
    handleDelete(id){
      this.projects = this.projects.filter((project)=>{
        return project.id !== id
      })
    },

    handleComplete(id){
      const p = this.projects.find((project)=>{
        return project.id === id
      })
      p.complete= !p.complete
    }
  }
}
</script>
