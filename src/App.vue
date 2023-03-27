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
  display: flex;
  width: min(100%, 1024px);
  border: 1px solid blue;
  margin: 0 auto;
  justify-content: space-around;
  flex-wrap: wrap;
}
.addButton {
  width: 225px;
  height: 120px;
  background: #696969;
  border: none;
  color: #9E9E9E;
  font-size: 2rem;
  margin: 10px auto;
}
.addButton:hover {
  color: white;
}
</style>
