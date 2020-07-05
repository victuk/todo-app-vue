<template>
<div>
<div>Welcome to my Task Tracker App</div>
<div class="tasksBoard">

<div class="taskLists">
<div>Completed Tasks</div>
<div v-for="task in doneTasks" :key="task.taskID">
{{ task.taskBody }}<br />
<button @click="doneTasks">In Progress</button>
<button>Delete</button>
</div>
</div>

<div class="taskLists">
<div>Tasks In Progress</div>
<div v-for="task in inProgress" :key="task.taskID">
{{ task.taskBody }}<br />
<button>{{task.taskButton1value}}</button>
<button>{{task.taskButton2value}}</button>
</div>
</div>

<div class="taskLists">
<div>Not completed Tasks</div>
<div v-for="task in notDone" :key="task.taskID">
{{ task.taskBody }}<br />
<button @click="inProgressMethod(task.taskID)">{{task.taskButton1value}}</button>
<button>{{task.taskButton2value}}</button>
</div>
</div>

</div>

<div>
<input type="text" v-model="newTaskBody"><br />
<button @click="addTask">Add Task</button>
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
      tasks: [
        { taskID: 1,
          taskBody: 'Wash the roof',
          taskStatus: 'not-done',
          taskButton1: '',
          taskButton2: '',
          taskButton1value: 'In Progress',
          taskButton2value: 'Complete',
        },
        { taskID: 1,
          taskBody: 'Wash the roof',
          taskStatus: 'in-progress',
          taskButton1: '',
          taskButton2: '',
          taskButton1value: 'Suspend',
          taskButton2value: 'Mark As Completed',
        },
      ],
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
          taskID: this.tasks.length + 1,
          taskBody: this.newTaskBody,
          taskStatus: 'not-done',
          taskButton1: 'inProgressMethod',
          taskButton2: 'completed',
          taskButton1value: 'In Progress',
          taskButton2value: 'Complete',
        },
        this.newTaskBody = '',
        );
      }
    },
    inProgressMethod(key) {
      // eslint-disable-next-line
      console.log(key);
    },
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
