<template>
  <div class="project" :class="{completed:project.complete}">
    <div class="actions">
      <h3 @click="toggleDetails">{{project.title}}</h3>
      <div class="icons">
        <router-link :to="{name: 'EditProject', params:{id:project.id}}">
          <span class="material-icons">edit</span>
        </router-link>
        <span @click="deleteProject" class="material-icons">delete</span>
        <span @click="toggleCompleted" class="material-icons tick">done</span>
      </div>
    </div>
    <div class="details">
      <p v-if="showDetails">{{project.details}}</p>
    </div>
  </div>
</template>

<script>

export default {

  name: 'SingleProject',

  props: ['project'],

  data() {
    return{
      showDetails: false,
      uri: 'http://localhost:3000/projects/' + this.project.id
    }
  },

  methods: {
    toggleDetails(){
      this.showDetails = !this.showDetails
    },

    deleteProject(){
    fetch(this.uri,{method: 'DELETE'})
      .then(()=>{this.$emit('delete',this.project.id)})
      .catch((err)=>console.log(err))
    },

    toggleCompleted() {
      fetch(this.uri,{
        method: 'PATCH',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify({
          complete: !this.project.complete
        })
      }).then(()=>{this.$emit('complete',this.project.id)})
      .catch((err)=>console.log(err))
    }
  },

}
</script>

<style scoped>
  .project{
    background: white;
    border-left:4px solid #e90074;
    border-radius: 5px;
    padding: 10px 20px;
    margin: 20px;
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
    margin-left: 10px;
    opacity: 0.5;
    cursor: pointer;
  }
  .material-icons:hover {
    opacity: 1;
  }
  .project.completed {
    border-left: 5px solid green;
  }
  .project.completed .tick{
    color: green;
  }
</style>