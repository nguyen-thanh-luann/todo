<template>
  <Addtodo v-on:add-todo="addnewTodo" />
  <TodoItem
    v-for="todo in todos"
    v-bind:key="todo.id"
    v-bind:todoProps="todo"
    v-on:item-completed="markComplete"
    v-on:item-delete="deleteTodo"
  />
</template>

<script>
import { ref } from 'vue';
import TodoItem from './TodoItem.vue';
import Addtodo from './AddTodo.vue';
// npm i uuid -> it make an unique id
// import { v4 as uuidv4 } from 'uuid';

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Todo',
  components: { TodoItem, Addtodo },
  setup() {
    let todoList = localStorage.getItem('todoList');

    const todos = todoList ? ref(JSON.parse(todoList)) : ref([]);

    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        localStorage.setItem('todoList', JSON.stringify(todos.value));
        return todo;
      });
    };

    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => todo.id !== id);
      localStorage.setItem('todoList', JSON.stringify(todos.value));
    };

    const addnewTodo = (newTodo) => {
      todos.value.push(newTodo);
      localStorage.setItem('todoList', JSON.stringify(todos.value));
    };

    return {
      todos,
      markComplete,
      deleteTodo,
      addnewTodo,
      todoList,
    };
  },
};
</script>

<style></style>
