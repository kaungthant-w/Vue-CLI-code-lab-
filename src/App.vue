<template>
  <div class="App">
    <h1 class="text-center bg-primary text-white p-3">{{title}}'s todo list</h1>
    <div class="container">
      <div class="row my-3">
        <div class="col">
          <input type="text" class="form-control" v-model="newTask" v-on:keyup.enter="addTasks">
        </div>
        <div class="col">
          <input type="button" value="Add Task" class="btn btn-secondary" v-on:click="addTasks">
        </div>
        <div class="col">
          <input type="button" value="Delete Tasks" class="btn btn-warning" @click="deleteTasks">
        </div>
      </div>

      <div v-if="filterTask.length > 0">
        <div class="row">
            <div class="col fs-3">Tasks</div>
            <div class="col-2 fs-3">Done</div>
          {{ filterTask.length }}
        </div>
        <div class="row" v-for="(task, index) in filterTask" v-bind:key="index">
            <!-- <div class="col">{{ task }}</div> -->
            <!-- <div class="col">{{ index }}</div> -->
            <!-- <div class="col-2">{{ task.done }}</div> -->

            <div class="col" :class="task.done ? 'delete':''">{{ task.action }}</div>
            <div class="col-2">
              <input  type="checkbox" v-model="task.done">
            </div>
        </div>
      </div>

      <!-- <div class="alert alert-warning text-center" v-else>There is no data.</div> -->
      <div class="alert alert-warning text-center mt-5" v-else-if="filterTask.length == 0">There is no data.</div>
      
      <div class="bg-danger text-white text-center p-2 mt-4 d-flex justify-content-around">
        <h5>Hide Completed Tasks</h5>
        <input type="checkbox" v-model="hideCompletedTask">
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'App',
    data: () => ({
      title:"CODE LAB",
      hideCompletedTask:false,
      newTask:'',
      tasks: []
    }),
    computed : {
      filterTask() {
        return this.hideCompletedTask ? this.tasks.filter((v) => !v.done) : this.tasks;
      }
    }
    ,
    methods : {
      addTasks() {
        // alert('click');
        // alert(this.newTask);
        if(this.newTask === '') {
          alert('Please add a task!');
        }

        // alert("ok you can");
        // alert(this.newTask);
        this.tasks.push({
          action:this.newTask,
          done:false,
        });

        this.storeData();
        this.newTask = '';
      },

      deleteTasks() {
        this.tasks = this.tasks.filter(v => !v.done);
        this.storeData();
      },

      storeData() {
        localStorage.setItem('myLocalTasks', JSON.stringify(this.tasks));
      }
    },

    // beforeCreate(){
    // console.log('before created running');
    // },
    // mounted(){
    //   console.log('mounted running');
    // },
    // beforeMount(){
    //   console.log('before mounted running');
    // },
    // created(){
    //   console.log('created running');
    // },

    mounted() {
      let data = localStorage.getItem('myLocalTasks');
      // console.log(data);
      if(data !== null) {
        this.tasks = JSON.parse(data);
      }
    },

  }
</script>


<style>
  .delete {
    text-decoration: line-through;
  }
</style>
