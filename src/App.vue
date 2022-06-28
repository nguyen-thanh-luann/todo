<template>
  <div id="app">
    <Header />
    <Todo />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Todo from './components/Todo.vue';

export default {
  name: 'App',
  components: { Header: Header, Todo: Todo },
};
</script>

<style>
/* pc */
@media (min-width: 1024px) {
  #app {
    width: 70%;
    margin: auto;
  }
}

/* Tablet */
@media (min-width: 740px) and (max-width: 1023px) {
}

/* Mobile */
@media (max-width: 740px) {
  #app {
    width: 100%;
  }
}

#app {
  font-family: 'Helvetica', sans-serif;
  padding: 0.5rem;
}
</style>
