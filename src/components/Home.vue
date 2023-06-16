<template>
  <div class="main-wrapper">

    <Navbar></Navbar>
    <div class="container card shadow shadow-lg--hover">

      <h6 class="mt-3">{{ msg }}</h6>

      <!-- Input -->
      <div class="d-flex mt-5">
        <input v-model="task" type="text" class="form-control add-task-field" placeholder="Enter task" v-on:keydown.enter="submitTask">
        <button @click="submitTask" class="btn btn-success rounded-0">ADD</button>
        
      </div>      

      <!-- Task Table -->
      <table class="table table-bordered mt-3">
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
            <td>
              <span :class="{'finished': task.status === 'finished'}">
                {{ task.name }}
              </span>
            </td>
            <td style="width: 120px;">
              <span @click="changeStatus(index)" class="pointer"
                :class="{'text-danger': task.status === 'to-do', 
                'text-warning': task.status === 'in-progress',
                'text-success': task.status === 'finished'
              }">
                {{ firstCharUpper(task.status) }}
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
  </div>
  
</template>

<script>

  import navbar from "./Navbar";
import Navbar from "./Navbar.vue";

  const STORAGE_KEY = 'vue-todo-app-storage';

  export default {
    components: {
    navbar,
    Navbar
},
    name: 'Home',
    
    props: {
      
    },
    data() {
      return {      
        msg: 'TODO-LIST',
        task: '',
        editedTask: null,
        availableStatuses: ['to-do', 'in-progress', 'finished'],
        tasks: [
          // {
          //   name: 'Read Vuejs2.0 documentation',
          //   status: 'to-do'
          // },
          // {
          //   name: 'Learning korean language',
          //   status: 'to-do'
          // },
          // {
          //   name: 'Creating vue project',
          //   status: 'in-progress'
          // }
        ]
      }
    },
    created(){
      console.log("this is created func");    
      this.tasks = JSON.parse(localStorage.getItem(STORAGE_KEY) || '[]');
    },
    methods: {
      submitTask(){
        console.log("submit");
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
        
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
        this.task = '';

      },

      deleteTask(index){
        this.tasks.splice(index, 1);
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
      },

      updateTask(index){
        this.task = this.tasks[index].name;
        this.editedTask = index;        
      },

      changeStatus(index){
        let nextIndex = this.availableStatuses.indexOf(this.tasks[index].status);      
        if(++nextIndex > 2) nextIndex = 0;      
        this.tasks[index].status = this.availableStatuses[nextIndex];
        localStorage.setItem(STORAGE_KEY, JSON.stringify(this.tasks));
      },

      firstCharUpper(str){
        return str.charAt(0).toUpperCase() + str.slice(1);
      },
      

    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main-wrapper {
  height: 100%;
  padding-top: 50px;
}

h1,
h2,h6 {
  font-weight: normal;
  color: rgb(32, 178, 44);
}
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}
.add-task-field{
  border-radius: 0;
  /* border: none; */
  background: transparent;
  border: 1px solid #11cdef;
}
th {
  background-color: #c2e2c6;
}

</style>
