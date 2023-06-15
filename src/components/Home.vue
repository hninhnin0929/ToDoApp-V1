<template>
  <div class="container">

    <h2 class="text-center mt-5">{{ msg }}</h2>

      <!-- Input -->
    <div class="d-flex">
      <input type="text" class="form-control" placeholder="Enter task">
      <button class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Home',
  data () {
    return {
      msg: 'Welcome to My Todo App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
</style>
