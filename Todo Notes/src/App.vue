<script setup>
import { ref } from 'vue'

const input = ref('')
const todos = ref([])

function add_todo() {
  if (input.value !== '') {
    todos.value.push(input.value);
    input.value = '';
  }
}
function remove(i) {
  todos.value.splice(i, 1);
}
function clear() {
  todos.value = [];
}
</script>

<template>
  <!-- main body -->
  <section id="todoapp">
    <!-- input -->
    <header class="header">
    <h1> Todo </h1>
    <input
      class="new-todo" 
      placeholder="type new missions" 
      autocomplete="off" 
      autofocus="autofocus" 
      v-model="input" 
      @keyup.enter="add_todo()"
    />
    </header>
    <!-- list -->
    <section class="main">
      <ul class="todo-list">
        <li class="todo" v-for="(item,index) in todos">
          <div class="view">
            <span class="index">{{ index + 1 }}</span>
            <label>{{ item }}</label>
            <button class="destroy" @click="remove(index)"></button>
          </div>
        </li>
      </ul>
    </section>
    <!-- footer -->
    <section class="footer" v-show="todos.length !== 0">
      <span class="todo-count">
        {{ todos.length }} items left
      </span>
      <button class="clear-completed" @click="clear()">
        Clear
      </button>
    </section>
  </section>
</template>

<style>
  @import "./assets/style.css";
</style>