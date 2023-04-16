<template>
  <div class="home">
    <v-container>
      <v-row>
        <v-col cols="10">
          <v-text-field
            name="name"
            label="label"
            id="id"
            v-model="taskTextField"
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-btn block color="success" @click="addTask">Add</v-btn>
        </v-col>
      </v-row>
      <TodoList :todos="todos"/>
    </v-container>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList";
export default {
  name: "Home",
  components: {
    TodoList,
  },
  data() {
    return {
      taskTextField: "",
      todos: [
        { id: 1, title: "Task 1", completed: false },
        { id: 2, title: "Task 2", completed: true },
        { id: 3, title: "Task 3", completed: false },
        { id: 4, title: "Task 4", completed: false },
      ],
    };
  },
  methods: {
    addTask() {
      const id = this.todos.length + 1;
      this.todos.push({
        id: id,
        title: this.taskTextField,
        completed: false,
      });
      this.taskTextField = "";
    },
  },
};
</script>
