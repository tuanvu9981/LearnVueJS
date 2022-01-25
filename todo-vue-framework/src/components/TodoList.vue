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
      v-bind:todo_props="todo"
      v-on:item-complete="markComplete"
      @delete-item="deleteOneItem"
    />
    <!-- markComplete will receive the id-data from emit function  -->
  </div>
</template>

<script>
import { ref } from "vue";
import TodoItem from "./TodoItem";

export default {
  name: "TodoList",
  components: { TodoItem },
  setup() {
    const todoList = ref([
      { id: 1, name: "Learn Japanese", completed: false },

      { id: 2, name: "Coding Vue", completed: true },

      { id: 3, name: "Write API", completed: false },
    ]);

    const markComplete = (id) => {
      // console.log(id);
      // console.log(todoList.value); --> cannot print todoList.value.target ...
      todoList.value = todoList.value.map((item) => {
        if (item.id === id) item.completed = !item.completed;
        return item;
      });
    };

    const deleteOneItem = (id) => {
      console.log(id);
      todoList.value = todoList.value.filter((item) => item.id !== id);
    };

    return {
      todoList,
      markComplete,
      deleteOneItem,
    };
  },
};
</script>

<style>
</style>