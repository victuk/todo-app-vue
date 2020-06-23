<template>
<div>
<div>Welcome to my Task Tracker App</div>
<div class="tasksBoard">

<div class="taskLists">
<div>Completed Tasks</div>
<div v-for="task in doneTasks" :key="task.taskID">
{{ task.taskBody }}<br />
<button>In Progress</button>
<button>Delete</button>
</div>
</div>

<div class="taskLists">
<div>Tasks In Progress</div>
<div v-for="task in inProgress" :key="task.taskID">
{{ task.taskBody }}<br />
<button>Suspend</button>
<button>Completed</button>
</div>
</div>

<div class="taskLists">
<div>Not completed Tasks</div>
<div v-for="task in notDone" :key="task.taskID">
{{ task.taskBody }}<br />
<button>{{inProgress}}</button>
<button>{{Completed}}</button>
</div>
</div>

</div>

<div>
<input type="text" :value="newTaskBody"><br />
<input type="text" :value="newTaskBody">
</div>

</div>
</template>

<script>
import '../assets/stylesheets/home.css';

export default {
  name: 'Home',
  data() {
    return {
      btnValue: ['Completed', 'In Progress', 'Done'],
      tasks: [
        {
          taskID: 1,
          taskBody: 'Wash the roof',
          taskStatus: 'not-done',
          Completed: '',
          inProgress: '',
          Donee: '',
        },
        { taskID: 2, taskBody: 'Take the generator to the hospital', taskStatus: 'in-progress' },
        { taskID: 3, taskBody: 'Slap my boss', taskStatus: 'done' },
        { taskID: 4, taskBody: 'Wash the roof', taskStatus: 'not-done' },
        { taskID: 5, taskBody: 'Take the generator to the hospital', taskStatus: 'in-progress' },
        { taskID: 6, taskBody: 'Slap my boss', taskStatus: 'done' },
        { taskID: 7, taskBody: 'Wash the roof', taskStatus: 'not-done' },
        { taskID: 8, taskBody: 'Take the generator to the hospital', taskStatus: 'in-progress' },
        { taskID: 9, taskBody: 'Slap my boss', taskStatus: 'done' },
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
    //
  },
};

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
