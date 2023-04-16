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
export default {
  name: "Home",
  components: {
    TodoAdd,
    TodoList,
  },
  data() {
    return {
      todos: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
        { id: 4, title: "Task 4", completed: false },
      ],
    };
  },
  methods: {
    addTask(task) {
      this.todos.push(task);
    },
    removeTask(id) {
      this.todos = this.todos.filter((item) => item.id !== id);
    },
  },
};
</script>
