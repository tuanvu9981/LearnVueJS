<template>
  <div id="app">
    <Header />
    <TodoList />.
  </div>
</template>

<script>
import Header from "./components/Header";
import TodoList from "./components/TodoList";
export default {
  name: "App",
  components: { Header, TodoList },
};
</script>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
}
</style>
