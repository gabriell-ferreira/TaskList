<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <task 
        :task='task' 
        v-for='(task, index) in tasks' :key="index" 
        @taskStateChanged='$emit("taskStateChanged", index)' 
        @removeTask='$emit("removeTask", index)'
      />
    </template>
    <template v-else>
      <p class="message">Sua vida está em dia :)</p>
    </template>
  </div>
</template>

<script>
import task from './task.component.vue'

export default {
  props: {
    tasks: {
      type: Array
    }
  },
  components: {
    task
  },
  methods: {
    
  }
}
</script>

<style>
  .task-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    margin: 3rem 0
  }

  .message {
    color: #ffffff;
    font-size: 1.5rem;
  }
</style>