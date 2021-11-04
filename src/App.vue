<template>
  <Header
    @toggle-add-task="toggleAddTask"
    title="Task Tracker"
    :showAddTask="showAddTask"
  />
  <div v-show="showAddTask">
    <AddTask @add-task="addTask" />
  </div>
  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    addTask(task) {
      this.tasks = [...this.tasks, task];
    },
    deleteTask(id) {
      if (confirm("are you sure?")) {
        this.tasks = this.tasks.filter((task) => task.id !== id);
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, reminder: !task.reminder } : task
      );
    },
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Walk the dog",
        day: "Nov 3 at 2:00pm",
        reminder: true,
      },
      {
        id: 2,
        text: "Take out the trash.",
        day: "Nov 5 at 10:30am",
        reminder: true,
      },
      {
        id: 3,
        text: "Call your sister.",
        day: "Nov 5 at 12:00pm",
        reminder: false,
      },
    ];
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
