<template>
  <div class="task">
    <p @click='taskStateChanged' v-if="task.pending" class="pending">
      {{task.name}}
      <span @click.stop="removeTask">X</span>
    </p>
    <p @click='taskStateChanged' v-else class="not-pending">
      {{task.name}}
      <span @click.stop="removeTask">X</span>
    </p>
  </div>
</template>

<script>
export default {
  data(){
    return {
      
    }
  },
  props: {
    task: {
      type: Object,
      required: true
    }
  },
  methods: {
    removeTask(){
      this.$emit('removeTask', this.task)
    },
    taskStateChanged(){
      this.$emit('taskStateChanged', this.task)
    }
  }
  
}
</script>

<style>
  .task {
    color: #ffffff;
  }

  .task p {
    margin: 0 1rem 2rem;
    padding: 3rem 5rem;

    border-top-right-radius: 1rem;
    border-bottom-left-radius: 1rem;

    font-size: 1.5rem;

    user-select: none;

    position: relative;

    transition: all ease .2s;
  }

  .task p span {
    position: absolute;
    top: 0.2rem;
    right: 0.2rem;

    display: flex;
    justify-content: center;
    align-items: center;

    border-radius: 50%;

    width: 2rem;
    height: 2rem;

    background: rgb(66, 57, 57);
    color: #ffffff;
    font-size: 1.3rem;

    cursor: pointer;

    transition: all ease .2s;
  }

  .task p span:hover {
    background: rgb(41, 34, 34);
    color: red;
  }

  .pending {
    background: rgb(190, 25, 25); 
    border-left: 1rem solid rgb(149, 12, 12);
  }

  .not-pending {
    background: rgb(4, 209, 14);
    border-left: 1rem solid rgb(11, 143, 6);
    text-decoration: line-through;
  }
</style>