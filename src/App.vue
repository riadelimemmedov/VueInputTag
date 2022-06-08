<template>
  <div class="container">
      <app-tags v-model="tags" :color="`bg-danger border rounded`"></app-tags>
  </div>
</template>

<script>
  import Tags from './components/Tags.vue'
  export default {
    data(){
      return{
        tags:'Vue.js,React.js'
      }
    },
    components:{
      'app-tags':Tags
    }
  }
</script>

<style>
  body{
    font-family: sans-serif;
  }
</style>
