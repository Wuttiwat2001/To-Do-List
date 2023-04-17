<template>
  <div class="home">
    <v-container>
      <TodoAdd @onSubmit="addTask" />
      <TodoList @onRemove="removeTask" :todos="todos" />
    </v-container>
  </div>
</template>

<script>
import TodoAdd from "@/components/TodoAdd.vue";
import TodoList from "@/components/TodoList";
import axios from "axios";
export default {
  name: "Home",
  components: {
    TodoAdd,
    TodoList,
  },
  data() {
    return {
      todos: [],
      todos_mockup: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
        { id: 4, title: "Task 4", completed: false },
      ],
    };
  },
  methods: {
    async addTask(task) {
      const res = await axios.post("https://jsonplaceholder.typicode.com/todos", task);
      this.todos.push(res.data)
    },
    removeTask(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
    async fetchApi() {
      const res = await axios.get("https://jsonplaceholder.typicode.com/todos");
      this.todos = res.data;
    },
  },
  mounted() {
    this.fetchApi();
  },
};
</script>
