<template>
  <li>
    <span v-bind:class="{done: todo.completed}">
      <label>
        <input type="checkbox" v-on:change="todo.completed = !todo.completed;" />
        <div class="check"></div>
      </label>
      <strong>{{index + 1}}</strong>
      {{todo.title | upperCase}}
    </span>
    <button v-on:click="$emit('remove-todo', todo.id)" class="rm" type="button">&times;</button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    index: Number
  },
  filters: {
    upperCase(value){
      return value.toUpperCase()
    }
  }
};
</script>

<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  justify-content: space-between;
  padding: 0.5rem 2rem;
  margin-bottom: 1rem;
}

span{
    flex-grow: 1;
    text-align: left;
}

.rm {
  background-color: #f66;
  color: bisque;
  font-weight: bold;
  border: 4px solid firebrick;
  box-shadow: 1px 1px 2px 0 #333;
  cursor: pointer;
  align-self: center;
}

input[type="checkbox"] {
  opacity: 0;
  height: 1px;
  width: 1px;
  position: absolute;
  z-index: -1;
}
input[type="checkbox"]:checked + .check{
   background-color: #2f2; 
}

.check {
  display: inline-block;
  height: 20px;
  vertical-align: middle;
  width: 20px;
  margin-right: 15px;
  background-color: #afa;
  border: 2px solid #333;
  border-radius: 6px;
  transition: background-color 0.3s cubic-bezier(0.3, 0, 0.7, 4);
}

.done{
    text-decoration: line-through solid black;
}
</style>