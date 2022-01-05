<template>
  <div class="form">
    <form @submit.prevent="handleSubmit">
      <label>title:</label>
      <input type="text" v-model="title" required>
      <label>Details:</label>
      <textarea v-model="details"></textarea>
      <button>Add Project</button>
    </form>
  </div>
</template>

<script>
export default {

  name: 'AddProject',

  components: {

  },
  
  data() {
    return{
      title: '',
      details: '',
    }
  },

  methods: {

    handleSubmit() {
      const project= {
        title: this.title,
        details: this.details,
        complete: false
      }

      fetch('http://localhost:3000/projects',{
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(project)
      }).then(()=>{this.$router.push({name: 'Home'})})
        .catch((err)=>console.log(err))
    }
  }
}
</script>

<style scoped>
  .form {
    background: white;
    padding: 20px;
    border-radius: 8px;
  }
  label {
    display: block;
    text-transform: uppercase;
    font-weight: bold;
    opacity: 0.5;
    font-size: 14px;
    letter-spacing: 1px;
    margin: 20px 0 10px 0;
  }
  input {
    width: 100%;
    border:none;
    border-bottom: 1px solid #f2f2f2;
    padding: 10px;
    box-sizing:border-box;
  }
  textarea {
    width: 100%;
    height: 100px;
    display: block;
    border: 1px solid #f2f2f2;
    padding: 10px;
    box-sizing: border-box;
  }
  button {
    display: block;
    background: #00ce89;
    border: none;
    border-radius: 4px;
    color: white;
    margin: 20px auto 0 auto;
    padding: 10px 5px;
    font-size: 16px;
  }

</style>