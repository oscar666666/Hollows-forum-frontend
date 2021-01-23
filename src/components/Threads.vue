<template>
  <div>
    <div class="container">
      <div class="row">
        <div class="col">
          <NewThreadModal />
        </div>
        <div class="col-8"></div>
        <div class="col"></div>
      </div>
    </div>

    <div class="Thread-data">
      <div class="column">
        <div>
          <b-card
            v-for="ThreadData in ThreadsList"
            :key="ThreadData.id"
            :title="ThreadData.Title"
            :sub-title="ThreadData.u_id"
            :footer="ThreadData.Post_time"
            align="left"
          >
            <b-card-text>
              {{ ThreadData.body }}
            </b-card-text>
          </b-card>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import NewThreadModal from "../components/NewThreadModal";

export default {
  name: "Threads",
  components: {
    NewThreadModal,
  },
  data() {
    return {
      ThreadsList: [],
      show: true,
    };
  },
  mounted() {
    axios({
      method: "GET",
      url: "http://127.0.0.1:8000/Thread/get_thread",
    }).then(
      (result) => {
        this.ThreadsList = result.data;
      },
      (error) => {
        console.error(error);
      }
    );
  },
};
</script>

<style>
.column {
  float: left;
  width: 66.3%;
  padding: 15px;
}
</style>
