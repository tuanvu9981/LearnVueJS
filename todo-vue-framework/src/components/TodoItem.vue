<template>
  <!-- <p class="todo-item completed" :id="id"> -->
  <p :class="['todo-item', props.completed ? 'completed' : '']">
    <input type="checkbox" :checked="props.completed" />
    {{ props.name }}
    <button class="del-btn">Delete</button>
  </p>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["props"],
};
</script>

<style>
.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  /* change pointer to hand-shape  */

  float: right;
}

.completed {
  text-decoration: line-through;
}

.todo-item {
  background: #f4f4f4;
  padding: 12px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}
</style>