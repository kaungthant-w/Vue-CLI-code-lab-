<template>
  <div class="App">
    <h1 class="text-center bg-primary text-white p-3">CODE LAB's todo list</h1>
    <div class="container">
      <div class="row">
        <div class="col fs-3">Tasks</div>
        <div class="col-2 fs-3">Done</div>
      </div>
      <div class="row" v-for="(task, index) in tasks" v-bind:key="index">
        <!-- <div class="col">{{ task }}</div> -->
        <!-- <div class="col">{{ index }}</div> -->
        <div class="col">{{ task.action }}</div>
        <div class="col-2">{{ task.done }}</div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name:'App',
    data: () => ({
      name:"Kyaw Kyaw",
      tasks: [
        {action:"Buy new phone", done:false},
        {action:"Get Shoes", done:true},
        {action:"Call Aung Aung", done:false},
        {action:"Buy new Shirt", done:false},
        {action:"Buy new Phone", done:true},
      ]
    }),
  }
</script>

<style>

</style>
