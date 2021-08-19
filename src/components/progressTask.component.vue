<template>
  <div class="progress">
    <div class="percent">
      {{progress}}%
    </div>
    <div class="bar" :style="{width: progress+'%'}">
    </div>
  </div>
</template>

<script>
export default {
  props: {
    progress: {
      type: Number
    }
  }
}
</script>

<style scoped>
  .progress {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;

    width: 33rem;
    height: 2rem;
    margin-bottom: 3rem;

    color: #ffffff;
    border: 3px solid #ffffff;
    border-bottom-right-radius: 1rem;
    border-top-left-radius: 1rem;
  }

  .bar {
    position: absolute;
    left: 0;

    width: 100%;
    height: 1.65rem;

    background-color: rgb(63, 189, 46);
    border-bottom-right-radius: 1rem;
    border-top-left-radius: 1rem;

    transition: width ease 1s;
    animation: animate 2s infinite alternate;
  }

  .percent {
    font-weight: bold;
    z-index: 1;
  }

  @keyframes animate {
    to {
      background-color: rgb(63, 189, 46);;
    } from {
      background: rgb(18, 105, 6);;
    }
  }

  @media (max-width: 600px){
    .progress {
      width: 23rem
    }
  }
</style>