<template>
<div>
<div>Welcome to my Task Tracker App</div>
<div class="tasksBoard">

<div class="taskLists">
<div>Completed Tasks</div>
<div v-for="task in doneTasks" :key="task.taskID">
{{ task.taskBody }}<br />
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton1value}}</button>
<button @click.prevent="deleteTask(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>

<div class="taskLists">
<div>Tasks In Progress</div>
<div v-for="task in inProgress" :key="task.taskID">
{{ task.taskBody }}<br />
<button @click.prevent="inProgressMethod(task.taskID)">{{task.taskButton1value}}</button>
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>

<div class="taskLists">
<div>Not completed Tasks</div>
<div v-for="task in notDone" :key="task.taskID">
{{ task.taskBody }}<br />
<button @click.prevent="inProgressMethod(task.taskID)">{{task.taskButton1value}}</button>
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>

</div>

<div>
<input type="text" v-model="newTaskBody"><br />
<button @click.prevent="addTask">Add Task</button>
</div>
</div>
</template>

<script>
import '../assets/stylesheets/home.css';

export default {
  name: 'Home',
  data() {
    return {
      newTaskBody: '',
      tasks: [],
    };
  },
  computed: {
    doneTasks() {
      return this.tasks.filter(task => task.taskStatus === 'done');
    },
    inProgress() {
      return this.tasks.filter(task => task.taskStatus === 'in-progress');
    },
    notDone() {
      return this.tasks.filter(task => task.taskStatus === 'not-done');
    },
  },
  methods: {
    addTask() {
      if (this.newTaskBody === '') {
        // eslint-disable-next-line
        alert('Please put something valid');
      } else {
        this.tasks.push({
          taskID: this.tasks.length,
          taskBody: this.newTaskBody,
          taskStatus: 'not-done',
          taskButton1value: 'In Progress',
          taskButton2value: 'Complete',
        },
        this.newTaskBody = '',
        );
      }
    },
    inProgressMethod(key) {
      // eslint-disable-next-line
      console.log(this.tasks[key]);
      // eslint-disable-next-line
      console.log(key);
      if (this.tasks[key].taskStatus === 'not-done') {
        this.tasks[key].taskStatus = 'in-progress';
        this.tasks[key].taskButton1value = 'Move to Not Completed';
        this.tasks[key].taskButton2value = 'Mark As Completed';
      } else if (this.tasks[key].taskStatus === 'in-progress') {
        this.tasks[key].taskStatus = 'not-done';
        this.tasks[key].taskButton1value = 'In Progress';
        this.tasks[key].taskButton2value = 'Complete';
      }
    },
    notComplete(key) {
      // eslint-disable-next-line
      console.log(this.tasks[key]);
      // eslint-disable-next-line
      console.log(key);
      if (this.tasks[key].taskStatus === 'not-done' || this.tasks[key].taskStatus === 'in-progress') {
        this.tasks[key].taskStatus = 'done';
        this.tasks[key].taskButton1value = 'Move to Progress Tab';
        this.tasks[key].taskButton2value = 'Delete Task';
      } else if (this.tasks[key].taskStatus === 'done') {
        this.tasks[key].taskStatus = 'in-progress';
        this.tasks[key].taskButton1value = 'Move to Not Completed';
        this.tasks[key].taskButton2value = 'Mark As Completed';
      }
    },
    deleteTask(key) {
      this.tasks.forEach((task) => {
        // eslint-disable-next-line
        console.log(key);
        // eslint-disable-next-line
        console.log(task);
        // this.tasks.pop(this.tasks.taskBody);
      });
    },
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
