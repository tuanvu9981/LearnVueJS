<template>
  <div>
    <!-- 
    <p>1st thing</p>
    <p>2nd thing</p>
    <p>3rd thing</p> 
    -->

    <!-- <p v-for="todo in todoList" v-bind:key="todo">{{ todo }}</p> -->

    <TodoItem
      v-for="todo in todoList"
      v-bind:key="todo.id"
      v-bind:props="todo"
    />
  </div>
</template>

<script>
import { ref } from "vue";
import TodoItem from "./TodoItem";

export default {
  name: "TodoList",
  setup() {
    const todoList = ref([
      { id: 1, name: "Learn Japanese", completed: false },

      { id: 2, name: "Coding Vue", completed: true },

      { id: 3, name: "Write API", completed: false },
    ]);
    return {
      todoList,
    };
  },
  components: { TodoItem },
};
</script>

<style>
</style>