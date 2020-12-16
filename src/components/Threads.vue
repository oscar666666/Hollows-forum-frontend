<template>
  <div>
    <h1>Threads</h1>
    <div v-for="ThreadData in ThreadsList" :key="ThreadData.id" class="Thread-data">     
    <span>{{ThreadData.Title}}</span>
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
        axios({ method: "GET", "url": "http://127.0.0.1:8000/get_thread" }).then(result => {
                    
                    this.ThreadsList = result.data;
                }, error => {
                    console.error(error);
                });
      /* async DisplayThreads() {
        try {
            let res = await axios({
                url: 'http://127.0.0.1:8000/get_thread',
                method: 'GET',
                data: {
                      
                    }
                })
                this.ThreadsList = res.data
            }
            catch (err) {
                console.log(err);
                alert(`Error: ${err}`)
            }

      }*/
    }
}
</script>