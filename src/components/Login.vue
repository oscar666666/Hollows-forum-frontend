<template>
<div>
<div id="Empty" class = "bodycolumn">
</div>
<div id="Login" class = "bodycolumn">
    <b-form  v-if="show">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        description="We'll never share your email with anyone else."
      >
      <!-- @Login="onSubmit"type="email" -->
        <b-form-input
          id="input-1"
          v-model="form.email"
          required
          placeholder="Enter email"
        ></b-form-input>
      </b-form-group>

      <b-form-group id="input-group-2" label="Password:" label-for="input-2">
        <b-form-input
          id="input-2"
          v-model="form.password"
          type="password"
          required
          placeholder="Enter password"
        ></b-form-input>
      </b-form-group>

      <b-button type="button" v-on:click="login()" variant="primary">Login</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>

<div id="Empty" class = "bodycolumn">
</div>
</div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Login',
    data() {
      return {
        form: {
          email: '',
          password: ''
        },
        show: true
      }
    },
    methods: {
      async login() {
        //evt.preventDefault()
        try {
            let res = await axios({
                url: 'http://127.0.0.1:8000/api-token-auth/',
                method: 'POST',
                data: {
                        username: this.form.email,
                        password: this.form.password
                        //grant_type: 'password'
                    }
                })
                alert(`Token received: ${res.data.token}`)
                axios.defaults.headers.common['Authorization'] = `Bearer ${res.data.token}`
                localStorage.setItem('authkey', res.data.token)
                this.$router.push('/about')
            }
            catch (err) {
                console.log(err);
                alert(`Error: ${err}`)
            }
        }
    
      }
    }
  
</script>
<!-- -------------------------------------------- -->

<style>
/* Create three equal columns that floats next to each other */
.bodycolumn {
  float: left;
  width: 33.33%;
  padding: 15px;
}
</style>