<template>
  <div class="home">
    <v-container>
      <TodoAdd @onSubmit="addTask" />
      <TodoList @onRemove="removeTask" :todos="reversedTodo" />
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
  computed:{
    reversedTodo(){
      return this.todos.slice().reverse()
    }
  },
  mounted() {
    this.fetchApi();
  },
};
</script>
