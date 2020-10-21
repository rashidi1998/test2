<template>
  <div class="todo-item" v-bind:class="{ 'is-complete': todo.completed }">
    <p>
      <input type="checkbox" v-on:change="markComplete" /> {{ todo.title }}
      <button @click="$emit('del-todo', todo.id)" class="del">x</button>
    </p>
  </div>
</template>
<script>
export default {
  name: "Todoitem",
  props: ["todo"],
  methods: {
    markComplete() {
      this.todo.completed = !this.todo.completed;
    },
  },
};
</script>
<style scoped>
.todo-item {
  background: gray;
  padding: 10px;
  border-bottom: 1px #ccc dotted;
}
.is-complete {
  text-decoration: line-through;
}
.edl {
  background: red;
  padding: 5px 9px;
  color: white;
  border: none;
  border-radius: 50%;
  cursor: pointer;
  float: right;
}
</style>
