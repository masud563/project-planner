<template>
  <nav class="main-nav">
    <router-link :to="{name:'Home'}">Projects</router-link>
    <router-link :to="{name:'AddProject'}">Add Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
  .main-nav {
    text-align: center;
    margin: 40px 0;
  }
  .main-nav a{
    text-decoration: none;
    color: #999;
    font-size: 18px;
    margin: 0 10px;
  }
  a.router-link-active {
    border-bottom: 3px solid #00ce89;
    color: black;
  }
</style>