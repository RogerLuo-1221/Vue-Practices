<script setup>
import { ref } from 'vue'

const num = ref(0)

function add() {
  if (num.value < 10){
    num.value++
  }else{
    alert('cant be bigger')
  }
}

function sub() {
  if (num.value > 0){
    num.value--
  }else{
    alert('cant be smaller')
  }
}
</script>

<template>
  <div id="app">
    <div class="input-num">
      <button @click="sub()">-</button>
    <span>{{ num }}</span>
    <button @click="add()">+</button>
    </div>
  </div>
</template>

<style>
  @import './assets/style.css';
</style>