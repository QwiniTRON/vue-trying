<template>
  <div>
    <h2>TODO app</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodo" />
    <select v-model="filter">
      <option value="all">All</option>
      <option value="done">Completed</option>
      <option value="notdone">Uncomoleted</option>
    </select>
    <Loader v-if="loading" />
    <ToDo v-else-if="filteredTodos.length" v-bind:todos="filteredTodos" @remove-todo="removeTodo" />
    <p v-else>No todos</p>
  </div>
</template>
<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
import Loader from "@/components/Loader.vue";
export default {
  name: "App",
  components: {
    ToDo: TodoList,
    AddTodo,
    Loader
  },
  data() {
    return {
      todos: [],
      loading: true,
      filter: 'all'
    };
  },
  methods: {
    removeTodo(id) {
      this.todos = this.todos.filter(t => t.id != id);
    },
    addTodo(todo) {
      this.todos.push(todo);
    }
  },
  // watch: {
  //   filter(value){

  //   }
  // },
  computed: {
    filteredTodos(){
      if(this.filter === 'all'){
        return this.todos
      }else if(this.filter === 'done'){
        return this.todos.filter((t) => t.completed)
      } else{
        return this.todos.filter((t) => !t.completed)
      }
    }
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        setTimeout(
          function() {
            this.todos = json;
            this.loading = false;
          }.bind(this),
          650
        );
      });
  }
};
</script>

<style scoped>
select{
  display: block;
  margin-bottom: 5px;
}
</style>