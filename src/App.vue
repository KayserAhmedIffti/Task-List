<template>
  <div class="container">
    <Header @toggleAddTask="toggleAddTask" title="Task Tracker"
    :showAddTask="showAddTask"
        />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>

    <TasksComponent @toggle-reminder="toggleReminder"
     @delete-task="deleteTask" :tasks="tasks"
     /> 

  </div>
  <!-- :tasks is used in this component property-->

</template>

<script>
  import Header from "./components/Header";
  import TasksComponent from "./components/Tasks";
  import AddTask from "./components/AddTask";

  export default {
  name: 'App',

  components: {
    Header,
    TasksComponent,
    AddTask
  },

  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },

  methods:{
    toggleAddTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
      this.tasks = [...this.tasks,task]
    },
    
    deleteTask(id) {
      if(confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },

    toggleReminder(id) {
        this.tasks = this.tasks.map((task) =>
          task.id === id 
          ? {...task, reminder: !task.reminder} 
          : task
        )
      },
      
  },

  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Doctors Apoinment',
        day: 'March 1st at 2.30 p.m',
        reminder: true,
      },
       {
        id: 2,
        text: 'Meeting at University reunion',
        day: 'April 15th at 5.30 p.m',
        reminder: true,
      },
      {
        id: 3,
        text: 'Food Shopping',
        day: 'August 20th at 9.30 p.m',
        reminder: false,
      },
    ]
   }
  
  }
</script>

<style scoped>
  .container {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    color: #2c3e50;
    margin-top: 60px;
    border: 1px solid;
  }
</style>
