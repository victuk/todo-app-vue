<template>
<div>
<div class="taskTracker">Welcome to my Task Tracker App</div>

<div class="container">
<input type="text" v-model.trim="newTaskBody" class="margin-right: 2px;">
<button @click.prevent="addTask">Add Task</button>
</div>

<div class="tasksBoard container">

<div class="taskLists">
<div class="">Completed Tasks</div>
<div v-for="task in doneTasks" :key="task.taskID" class={taskstyle}>
<div :class="task.taskstyle">
{{ task.taskBody }}<br />
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton1value}}</button>
<button @click="deleteTask(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>
</div>

<div class="taskLists">
<div>Tasks In Progress</div>
<div v-for="task in inProgress" :key="task.taskID" class={taskstyle}>
<div :class="task.taskstyle">
{{ task.taskBody }}<br />
<button @click.prevent="inProgressMethod(task.taskID)">{{task.taskButton1value}}</button>
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>
</div>

<div class="taskLists">
<div>Not completed Tasks</div>
<div v-for="task in notDone" :key="task.taskID">
<div :class="task.taskstyle">
{{ task.taskBody }}<br />
<button @click.prevent="inProgressMethod(task.taskID)">{{task.taskButton1value}}</button>
<button @click.prevent="notComplete(task.taskID)">{{task.taskButton2value}}</button>
</div>
</div>
</div>

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
          taskstyle: 'not-done-style',
        },
        );
        this.newTaskBody = '';
      }
    },
    inProgressMethod(key) {
      if (this.tasks[key].taskStatus === 'not-done') {
        this.tasks[key].taskStatus = 'in-progress';
        this.tasks[key].taskButton1value = 'Move to Not Completed';
        this.tasks[key].taskButton2value = 'Mark As Completed';
        this.tasks[key].taskstyle = 'in-progress-style';
      } else if (this.tasks[key].taskStatus === 'in-progress') {
        this.tasks[key].taskStatus = 'not-done';
        this.tasks[key].taskButton1value = 'In Progress';
        this.tasks[key].taskButton2value = 'Complete';
        this.tasks[key].taskstyle = 'not-done-style';
      }
    },
    notComplete(key) {
      if (this.tasks[key].taskStatus === 'not-done' || this.tasks[key].taskStatus === 'in-progress') {
        this.tasks[key].taskStatus = 'done';
        this.tasks[key].taskButton1value = 'Move to Progress Tab';
        this.tasks[key].taskButton2value = 'Delete Task';
        this.tasks[key].taskstyle = 'completed-style';
      } else if (this.tasks[key].taskStatus === 'done') {
        this.tasks[key].taskStatus = 'in-progress';
        this.tasks[key].taskButton1value = 'Move to Not Completed';
        this.tasks[key].taskButton2value = 'Mark As Completed';
        this.tasks[key].taskstyle = 'in-progress-style';
      }
    },
    deleteTask(key) {
      /* eslint-disable */
      this.tasks.forEach((task) => {
        if(task.taskID === key) {
          // console.log(task);
          this.tasks.splice(task, 1);
        }
      });

    },
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
