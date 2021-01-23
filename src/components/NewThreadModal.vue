<template>
  <div>
    <b-button v-b-modal.modal-prevent-closing>Post New Thread</b-button>

    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Post Thread"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          label="Title"
          label-for="title-input"
          invalid-feedback="Title is required"
          :state="titleState"
        >
          <b-form-input
            id="title-input"
            v-model="form.title"
            :state="titleState"
            required
          ></b-form-input>
        </b-form-group>

        <b-form-group
          label="body"
          label-for="body-input"
          invalid-feedback="Body is required"
          :state="bodyState"
        >
          <b-form-input
            id="body-input"
            v-model="form.body"
            :state="bodyState"
            required
          ></b-form-input>
        </b-form-group>

      </form>
    </b-modal>
  </div>
</template>

<script>
import axios from 'axios'

  export default {
    data() {
      return {
          form: {
          title: '',
          body: ''
        }
      }
    },
    methods: {
      checkFormValidity() {
        const valid = this.$refs.form.checkValidity()
        this.titleState = valid
        this.bodyState = valid
        return valid
      },
      resetModal() {
        this.form.title = ''
        this.titleState = null
        this.form.body = ''
        this.bodyState = null
      },
      handleOk(bvModalEvt) {
        // Prevent modal from closing
        bvModalEvt.preventDefault()
        // Trigger submit handler
        this.handleSubmit()
      },
      handleSubmit() {
        // Exit when the form isn't valid
        if (!this.checkFormValidity()) {
          return
        }
        axios.post('http://127.0.0.1:8000/Thread/post_thread', {
          Title: this.form.title,
          body: this.form.body
         }, 
         {
            headers: {
            'Authorization': `token ${localStorage.getItem('authkey')}` 
            }
         }
         )
                .then(function(  ){
                    // Handle success
                }.bind(this));
        
        // Hide the modal manually
        this.$nextTick(() => {
          this.$bvModal.hide('modal-prevent-closing')
        })
      }
    }
  }
</script>