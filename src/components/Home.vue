<template>
  <div class="container">

    <h2 class="text-center mt-5">{{ msg }}</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="Enter task">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
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
          <td>{{ task.name }}</td>
          <td>
            <span @click="changeStatus(index)" class="pointer">
              {{ task.status }}
            </span>
          </td>
          <td>
            <div class="text-center" @click="updateTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
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
      task: '',
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress', 'finished'],
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
  },
  methods: {
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask === null){
        this.tasks.push(
          {
          name: this.task,
          status: 'to-do'
          }
        )
      }else{             
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      
      this.task = '';

    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    updateTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index){
      let nextIndex = this.availableStatuses.indexOf(this.tasks[index].status);      
      if(++nextIndex > 2) nextIndex = 0;      
      this.tasks[index].status = this.availableStatuses[nextIndex];
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
.pointer {
  cursor: pointer;
}
</style>
