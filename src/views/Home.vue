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
      <v-card>
        <v-card-title primary-title>
          <v-container>
            <v-row
              class="d-flex flex-row"
              v-for="(item, index) in todos"
              :key="index"
            >
              <v-col cols="12" class="d-flex flex-row align-center">
                <v-checkbox v-model="value" value="value"></v-checkbox>
                <span>{{ item.title }}</span>
                <v-spacer></v-spacer>
                <v-btn color="error">X</v-btn>
              </v-col>
              <v-col cols="12">
                <v-divider></v-divider>
              </v-col>
            </v-row>
          </v-container>
        </v-card-title>
      </v-card>
    </v-container>
  </div>
</template>

<script>
export default {
  name: "Home",
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
      this.taskTextField = ""
    },
  },
};
</script>
