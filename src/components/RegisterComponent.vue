<template>
  <div>
    <div id="Empty" class="bodycolumn"></div>
    <div id="Register" class="bodycolumn">
      <b-form v-if="show">
        <b-form-group
          id="input-group-1"
          label="Username:"
          label-for="input-1"
          description="Please enter your username"
        >
          <b-form-input
            id="input-1"
            v-model="form.username"
            required
            placeholder="Enter username"
          ></b-form-input>
        </b-form-group>
        <b-form-group
          id="input-group-1"
          label="Email address:"
          label-for="input-1"
          description="We'll never share your email with anyone else."
        >
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
        <b-form-group
          id="input-group-3"
          label="PasswordVerify:"
          label-for="input-2"
        >
          <b-form-input
            id="input-3"
            v-model="form.passwordVerify"
            type="password"
            required
            placeholder="Enter password"
          ></b-form-input>
        </b-form-group>
        <b-button type="button" v-on:click="Register()" variant="primary"
          >Register</b-button
        >
      </b-form>
      <b-card class="mt-3" header="Form Data Result">
        <pre class="m-0">{{ form }}</pre>
      </b-card>
    </div>

    <div id="Empty" class="bodycolumn"></div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "Login",
  data() {
    return {
      form: {
        username: "",
        email: "",
        password: "",
        passwordVerify: "",
      },
      show: true,
    };
  },
  methods: {
    async Register() {
      //evt.preventDefault()
      try {
        await axios({
          url: "http://127.0.0.1:8000/Register/",
          method: "POST",
          data: {
            username: this.form.username,
            email: this.form.email,
            password: this.form.password,
            passwordVerify: this.form.passwordVerify,
            //grant_type: 'password'
          },
        });
        alert(`Registration success`);

        this.$router.push("/about");
      } catch (err) {
        console.log(err);
        alert(`Error: ${err}`);
      }
    },
  },
};
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
