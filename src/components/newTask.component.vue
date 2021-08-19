<template>
  <div class="new-task">
    <input 
      type="text" 
      v-model="task.name" 
      placeholder="Insira uma tarefa" 
      @keydown.enter="addTask"
    >
    <button @click="addTask">+</button>
  </div>
</template>

<script>
export default {
  data(){
    return {
      task: {
        name: '',
        pending: ''
      }
    }
  },
  methods: {
    addTask(){
      if (this.task.name != ''){
        this.$emit('addTask', {
          name: this.task.name,
          pending: this.task.pending || true
        })
  
        this.task.name = ''
        document.querySelector('input').style.border = 'none'
      } else {
        document.querySelector('input').style.border = '5px solid red'
      }
    }
  }
}
</script>

<style scoped>
  .new-task {
    display: flex;
    align-items: center;
  }

  input {
    width: 30rem;
    height: 3rem;
    padding: 0 1rem;

    border-bottom-left-radius: 1rem;
    border: none;

    font-size: 1.5rem;

    outline: none;
  }

  button {
    height: 3rem;
    width:3rem;
    padding: 0;

    background-color: rgb(61, 216, 61);

    border: none;
    border-top-right-radius: 1rem;

    cursor: pointer;

    transition: background ease .2s;
  }

  button:hover {
    background-color: rgb(33, 148, 33);
  }

  .alert {
    position: absolute;
    top: 12rem;
    right: 40%;
    left: 40%;
  }

  @media (max-width: 600px){
    input {
      width: 20rem
    }
  }
</style>