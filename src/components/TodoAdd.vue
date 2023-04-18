<template>
  <v-row>
    <v-col cols="11">
      <v-text-field
        name="task"
        label="Add new Task"
        id="task"
        @keyup.enter="addTask"
        v-model="taskTextField"
      />
    </v-col>
    <v-col cols="1" class="d-flex flex justify-center">
      <v-btn
        color="primary"
        class="ma-2 white--text"
        :disabled="taskTextField.length < 1"
        fab
        @click="addTask"
      >
        <v-icon dark> mdi-plus-box </v-icon>
      </v-btn>
    </v-col>
  </v-row>
</template>
<script>
import { v4 as uuidv4 } from "uuid";
export default {
  name: "TodoAdd",
  data() {
    return {
      taskTextField: "",
    };
  },
  methods: {
    addTask() {
      if (this.taskTextField.length > 1) {
        const task = {
          id: uuidv4(),
          title: this.taskTextField,
          completed: false,
        };
        this.$emit("onSubmit", task);
        this.taskTextField = "";
      }
    },
  },
};
</script>
<style></style>
