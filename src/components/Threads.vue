<template>
  <div>

    <h1>Threads</h1>
    <div class="Thread-data">     
    <div class="column">
    <div>
    <b-card v-for="ThreadData in ThreadsList" 
            :key="ThreadData.id" 
            :title= 'ThreadData.Title' 
            :sub-title='ThreadData.u_id' 
            :footer='ThreadData.Post_time' 
            align="left">
    <b-card-text>
      {{ThreadData.body}}
    </b-card-text>

  </b-card>
</div>
</div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Threads',
    data() {
      return {
        ThreadsList: [],
        show: true
      }
    },
    mounted() {
        axios({ method: "GET", "url": "http://127.0.0.1:8000/Thread/get_thread" }).then(result => {
                    
                    this.ThreadsList = result.data;
                }, error => {
                    console.error(error);
                });
    }
}
</script>

<style>
.column {
  float: left;
  width: 66.3%;
  padding: 15px;
}
</style>