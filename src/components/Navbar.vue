<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-gradient-info">
      <div class="container justify-content-center ">
        <a class="navbar-brand" href="#">WELCOME ALL!!!</a>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data: function() {
    return {
      userLoggedIn: false
    };
  },
  methods: {
    
  },
  created() {
  },
};
</script>

<style>
.navbar-brand{
  font-size: 20px;
  color: rgb(255, 127, 138);
}
@media screen and (max-width: 768px) {
  .navbar .container{
    margin-top: 0.25rem !important;
  }
}
</style>
