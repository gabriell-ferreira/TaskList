<template>
  <div id="app">
    <h1>Task List</h1>
    <progressBar :progress='progress' />
    <newTask @addTask='add'/>
    <taskGrid 
      @taskStateChanged='toggleTaskState' 
      :tasks='tasks' 
      @removeTask='remove'
    />
    <footer>
      &copy;<a href="https://github.com/gabriell-ferreira">Gabriel Ferreira</a>
    </footer>
  </div>
</template>

<script>
import newTask from './components/newTask.component.vue'
import taskGrid from './components/taskGrid.component.vue'
import progressBar from './components/progressTask.component.vue'

export default {
  created() {
    const json = localStorage.getItem('tasks')
    const array = JSON.parse(json)
    this.tasks = Array.isArray(array) ? array : []
  },
  watch: {
    tasks: {
      deep: true,
      handler(){
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    }
  },
  computed: {
    progress(){
      const total = this.tasks.length
      const done = this.tasks.filter(task => !task.pending).length

      return Math.round(done / total * 100) || 0
    }
  },
  data(){
    return {
      tasks: []
    }
  },
  methods: {
    add(task){
      this.tasks.push({
        name: task.name,
        pending: task.pending
      })
    },
    remove(index){
      this.tasks.splice(index, 1)
    },
    toggleTaskState(index){
      this.tasks[index].pending = !this.tasks[index].pending 
    }
  },
  components: {
    newTask,
    taskGrid,
    progressBar
  }
}
</script>

<style scoped>
  #app {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    margin-top: 5rem;
  }

  h1 {
    color: #ffffff;
    margin-bottom: 3rem;
  }

  footer {
    color: #ffffff;
  }

  footer:hover {
    text-decoration: underline;
  }

  footer a {
    text-decoration: none;
    color: #ffffff;
    margin-left: .5rem;
  }
</style>