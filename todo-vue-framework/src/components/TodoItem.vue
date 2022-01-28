<template>
  <!-- <p class="todo-item completed" :id="id"> -->
  <p :class="['todo-item', todo_props.completed ? 'completed' : '']">
    <input
      type="checkbox"
      :checked="todo_props.completed"
      v-on:change="markAsCompleted"
    />
    {{ todo_props.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["todo_props"],
  // this props is an array containing a lot of element

  setup(props, context) {
    const markAsCompleted = () => {
      context.emit("item-complete", props.todo_props.id);
    };

    const deleteItem = () => {
      context.emit("delete-item", props.todo_props.id);
    };

    return { markAsCompleted, deleteItem };
  },
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