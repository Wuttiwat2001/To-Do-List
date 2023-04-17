<template>
  <div class="home">
    <v-container>
      <TodoAdd @onSubmit="addTask" />
      <TodoList
        @onEdit="editTask"
        @onRemove="removeTask"
        :todos="todos | reversed"
      />
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
      const res = await axios.post(
        "https://jsonplaceholder.typicode.com/todos",
        task
      );
      this.todos.push(res.data);
    },
    async removeTask(id) {
      const res = await axios.delete(
        `https://jsonplaceholder.typicode.com/todos/${id}`
      );
      if (res.status === 200) {
        this.todos = this.todos.filter((item) => item.id !== id);
      }
    },
    async fetchApi() {
      const res = await axios.get("https://jsonplaceholder.typicode.com/todos");
      this.todos = res.data;
    },
    editTask(task) {
      const newArray = this.todos.map((item) => {
        if (item.id !== task.id) {
          return item;
        }
        const editArray = { ...item };
        editArray.title = task.title
        return editArray
      });
      this.todos = newArray
    },
  },
  filters: {
    reversed(value) {
      return value.slice().reverse();
    },
  },
  mounted() {
    this.fetchApi();
  },
};
</script>
