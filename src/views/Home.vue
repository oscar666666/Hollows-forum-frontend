<template>
<div id="app">
    <Navigation/>
   <!-- <Login/> -->
    <router-view/>
    <Threads/>
  </div>
</template>

<script>
import Threads from '../components/Threads'  

  export default {   
    name: 'App',   
    components: {     
      Threads
      }
    }
</script>
