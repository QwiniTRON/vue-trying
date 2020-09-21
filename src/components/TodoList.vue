<template>
  <div>
    <ul>
      <TodoItem 
      v-for="(t, i) of todos" 
      v-bind:todo="t" 
      v-bind:index="i"
      v-on:remove-todo="removeTodo"
      />
    </ul>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
export default {
  components: {
    TodoItem
  },
  props: ["todos"],
  methods: {
      removeTodo(id){
          this.$emit('remove-todo', id)
      }
  }
};
</script>

<style scoped>
    ul{
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>