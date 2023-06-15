<template>
  <div class="container">

    <h2 class="text-center mt-5">{{ msg }}</h2>

    <!-- Input -->
    <div class="d-flex">
      <input type="text" class="form-control" placeholder="Enter task">
      <button class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th>{{ task.name }}</th>
          <td>{{ task.status }}</td>
          <td>
            <div class="text-center">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>

  </div>
</template>

<script>
export default {
  name: 'Home',
  props: {
    
  },
  data() {
    return {
      msg: 'Welcome to My Todo App',
      tasks: [
        {
          name: 'Read Vuejs2.0 documentation',
          status: 'to-do'
        },
        {
          name: 'Learning korean language',
          status: 'to-do'
        },
        {
          name: 'Creating vue project',
          status: 'in-progress'
        }
      ]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
</style>
