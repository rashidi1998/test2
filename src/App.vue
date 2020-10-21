<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="delTodo" />
  </div>
</template>

<script>
import header from "./components/layout/Header";
import Todos from "./components/Todos";
import AddTodo from "./components/AddTodo";
import axios from "axios";
export default {
  name: "App",
  components: {
    header,
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    delTodo(id) {
      axios
        .delete("http://jsonplaceholder.typicode.com/todos/ ${id}")
        .then(() => (this.todos = this.todos.filter((todo) => todo.id !== id)))
        .catch((err) => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("http://jsonplaceholder.typicode.com/todos", { title, completed })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console(err));
    },
  },
  created() {
    axios
      .get("http://jsonplaceholder.typicode.com/todos?_limit=5")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: opx;
  padding: opx;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line_height: 1.4;
}
btn {
  display: inline-block;
  border: none;
  background: gray;
  color: white;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: wheat;
}
</style>
