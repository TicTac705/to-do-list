<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo"/>
    <button>Add Todo</button>
  </form>

  <ul v-if="filteredTodos.length > 0">
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done">
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">X</button>
    </li>
  </ul>

  <h3 v-if="filteredTodos.length < 1">No content</h3>

  <button @click="hideCompleted = !hideCompleted">
    {{ hideCompleted ? 'Show all' : 'Hide completed' }}
  </button>
</template>

<script lang="ts">
import {Vue} from 'vue-class-component';
import {TodoInterface} from "@/interfaces/todo.interface";

export default class MainPage extends Vue {
  private id = 0;

  private newTodo = '';
  private hideCompleted = false;
  private todos: TodoInterface[] = [
    {id: this.id++, text: 'Learn HTML', done: true},
    {id: this.id++, text: 'Learn JavaScript', done: true},
    {id: this.id++, text: 'Learn Vue', done: false}
  ];

  get filteredTodos(): TodoInterface[] {
    if (this.hideCompleted) {
      return this.todos.filter((todo: TodoInterface) => !todo.done);
    }

    return this.todos;
  }

  addTodo() {
    this.todos.push({id: this.id++, text: this.newTodo, done: false});
    this.newTodo = '';
  }

  removeTodo(todo: TodoInterface) {
    this.todos = this.todos.filter((t) => t !== todo);
  }
}
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
