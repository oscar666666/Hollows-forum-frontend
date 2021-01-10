<template>
<div id="app">
    <Navigation/>
    <NewThreadModal/>
   <!-- <Login/> -->
    <router-view/>
    <Threads/>
  </div>
</template>

<script>
import Threads from '../components/Threads'  
import NewThreadModal from '../components/NewThreadModal'  

  export default {   
    name: 'App',   
    components: {     
      Threads,
      NewThreadModal  
      }
    }
</script>
