<script setup>
import StopWatch from './components/StopWatch.vue'
import { ref } from 'vue';

const timers = ref([1])
</script>

<template>
  <div class="App">
    <stop-watch v-for="timer in timers" :key="timer"/>
    <button class="addButton" @click="timers.push(Date.now())">
      +
    </button>
  </div>
</template>

<style>
.App {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 20px;
  width: min(100%, 675px);
  margin: auto;
  justify-content: space-around;
}
.addButton {
  height: 120px;
  background: #696969;
  border: none;
  color: #9E9E9E;
  font-size: 2rem;
}
.addButton:hover {
  color: white;
}

@media (max-width: 768px) {
  .App {
    width: min(100%, 450px);
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 480px) {
  .App {
    width: min(100%, 225px);
    grid-template-columns: repeat(1, 1fr);
  }
}
</style>
