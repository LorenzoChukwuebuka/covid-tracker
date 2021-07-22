<template>
   <Header/>
   <div class="container mx-auto"> </div>
  <router-view/>
</template>
<script>
import Header from "./components/header.vue"
export default {
  components:{
    Header,
  }
}
</script>

<style>
 
</style>
