<template>
  <div class="filter-project">
    <button @click="filterProject('all')" :class="{active: current==='all'}" >All</button>
    <button @click="filterProject('ongoing')" :class="{active: current==='ongoing'}" >Ongoing</button>
    <button @click="filterProject('completed')" :class="{active: current==='completed'}" >Completed</button>
  </div>
</template>

<script>
export default {

  name: 'FilterNav',

  props: ['current'],

  methods: {
    
    filterProject(by){
      this.$emit('filterProject', by)
    }
  }

}
</script>

<style scoped>
  .filter-project {
    margin: 10px 20px;
  }
  .filter-project button {
    border: none;
    background: none;
    color: #bbb;
    font-weight: bold;
    text-transform: uppercase;
    letter-spacing: 1px;
    padding: 0 15px;
    cursor: pointer;
  }
  .filter-project button.active {
    color: #555;
  }
</style>