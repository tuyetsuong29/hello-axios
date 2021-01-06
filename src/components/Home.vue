<template>
  <div class="home">
    <h1>Todos</h1>
    <div>
      <div><input type="text" v-model="todoName" @keyup.enter="addTodo" /></div>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          {{ todo.name }}
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import axios from "axios";
const baseURL = "http://localhost:3000/todos";
export default {
  name: "home",
  data() {
    return {
      todos: [],
      todoName: "",
    };
  },
  async created() {
    let result = await axios.get(`http://localhost:3000/todos`);
    this.todos = result.data;
  },
  methods: {
    async addTodo() {
      const res = await axios.post(baseURL, { name: this.todoName });
      this.todos = [...this.todos, res.data];
      this.todoName = "";
    },
  },
};
</script>
<style scoped>
.home {
  margin-left: 6rem;
}
</style>
