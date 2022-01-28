<template>
  <div>
    <!-- 
    <p>1st thing</p>
    <p>2nd thing</p>
    <p>3rd thing</p> 
    -->

    <!-- <p v-for="todo in todoList" v-bind:key="todo">{{ todo }}</p> -->

    <AddTodo
      @add-todo="addNewItem"
    />
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
//import {v4 as uuidv4} from 'uuid'
import axios from 'axios'
import TodoItem from "./TodoItem";
import AddTodo from "./AddTodo"

export default {
  name: "TodoList",
  components: { TodoItem, AddTodo },
  setup() {
    const todoList = ref([]);

    const getAllTodos = async () => {
      try {
        const res = await axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5');
        todoList.value = res.data; //asign value
      } catch (error) {
        console.log(error)
      }
    }

    getAllTodos();

    const markComplete = (id) => {
      // console.log(id);
      // console.log(todoList.value); --> cannot print todoList.value.target ...
      todoList.value = todoList.value.map((item) => {
        if (item.id === id) item.completed = !item.completed;
        return item;
      });
    };

    const deleteOneItem = async (id) => {
      // console.log(id);
      // todoList.value = todoList.value.filter((item) => item.id !== id);
      try {
        // delete backend 
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);

        // at the same time, delete front end 
        todoList.value = todoList.value.filter((item) => item.id !== id);
      } catch (error) {
        console.log(error)
      }
    };

    const addNewItem = async (newItem) => {
      try {
        const res = await axios.post('https://jsonplaceholder.typicode.com/todos',newItem);
        todoList.value.push(res.data);

      } catch (error) {
        console.log(error);
      }
      //todoList.value.push(newItem);
    }

    return {
      todoList,
      markComplete,
      deleteOneItem,
      addNewItem,
      getAllTodos,
    };
  },
};
</script>

<style>
</style>