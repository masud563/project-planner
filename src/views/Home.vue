<template>
  <FilterNav @filterProject="current=$event" :current="current" />
  <div v-if="projects.length">
    <div  v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
    </div>
  </div>
</template>

<script>
import FilterNav from '../components/FilterNav.vue'

import SingleProject from '../components/SingleProject.vue'
export default {
  name: 'Home',
  components: {
    SingleProject,
    FilterNav
  },
  
  mounted() {
    fetch('http://localhost:3000/projects')
      .then((res)=>res.json())
      .then((data)=>this.projects=data)
      .catch((err)=>{console.log(err.message)})
  },

  data() {
    return{
      projects: [],
      current: 'all'
    }
  },

  computed: {
    filteredProjects(){
      console.log(this.current)
      if(this.current === 'all'){
        return this.projects
      }
      else if(this.current === 'ongoing'){
        console.log(`else if`)
        return this.projects.filter((project)=>{
          return project.complete === false
        })
      }
        else {
          console.log(`else `)
          return this.projects.filter((project)=>{
           return project.complete === true
          })
        }
      
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
      p.complete = !p.complete
    }
  }
}
</script>
