<template>
  <div id="nav">
    <div class="container">
      <div class="row">
        <div class="col">
          <router-link to="/">Home</router-link> |
          <router-link to="/about">About</router-link>|
        </div>
        <div class="col-8"></div>
        <div class="col"><router-link to="/Login">Login</router-link>|</div>
                <div class="col"><router-link to="/Register">Register</router-link>|</div>

      </div>
    </div>

    <div class="container">
      <div class="row">
        <div class="col">
        </div>
        <div class="col-8"></div>
        <div class="col"></div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "App",
  
};
</script>
