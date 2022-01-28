<template>
  <form @submit="add_item">
      <input type="text" placeholder="New Todo" v-model="title"/>
      <input type="submit" value="Add" class="add-btn"/>
  </form>
</template>

<script>
import {ref} from 'vue'
// import {v4 as uuidv4} from 'uuid'

export default {
    name: "AddTodo",
    setup(props, context){
        const title = ref('');
        const add_item = (e) => {
            e.preventDefault();
            const newItem = {
                //id: uuidv4(),
                title: title.value,
                completed: false
            }

            context.emit("add-todo",newItem);

            title.value = '';
        }
        return {title, add_item}
    }
    
}
</script>

<style scoped>
.form{
    display: flex;
}

input[type="text"]{
    flex: 10; /* 10 line */
    padding: 5px /* each line 's gap*/

}

input[type="submit"]{
    flex: 2;
}
</style>