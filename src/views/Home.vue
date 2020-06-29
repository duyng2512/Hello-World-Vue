<template>
  <div>
    <div class="container">
      <AddTodo v-on:add-todo="addTodo" />
      <HelloWorld msg="Welcome to Your Vue.js App" />
      <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    </div>
  </div>
</template>

<script>
import Todos from '../components/Todo.vue';
import HelloWorld from '../components/HelloWorld.vue';
import AddTodo from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    HelloWorld,
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`http://localhost:3000/posts/${id}`)
        .then(() => (this.todos = this.todos.filter((item) => item.id !== id)))
        .catch((err) => console.log(err));
    },

    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post('http://localhost:3000/posts', {
          title,
          completed,
        })
        .then((res) => (this.todos = [...this.todos, res.data]))
        .catch((err) => console.log(err));
    },
  },
  created() {
    axios
      .get('http://localhost:3000/posts')
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
body {
  margin: 0px !important;
}
.container {
  padding: 1em;
}
.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
