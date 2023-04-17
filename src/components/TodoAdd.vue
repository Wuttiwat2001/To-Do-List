<template>
  <v-row>
    <v-col cols="11">
      <v-text-field
        name="name"
        label="Add new Task"
        id="id"
        @keyup.enter="addTask"
        v-model="taskTextField"
      ></v-text-field>
    </v-col>
    <v-col cols="1" class="d-flex flex justify-center">
      <v-btn
      color="primary"
      class="ma-2 white--text"
      fab
      @click="addTask"
    >
      <v-icon dark>
        mdi-plus-box
      </v-icon>
    </v-btn>
    </v-col>
  </v-row>
</template>
<script>
import { v4 as uuidv4 } from 'uuid';
export default {
  name: "TodoAdd",
  data(){
    return{
      taskTextField: "",
    }
  },
  methods:{
    addTask(){
      const task = {
        id: uuidv4(),
        title: this.taskTextField,
        completed: false
      }
      this.$emit("onSubmit", task)
      this.taskTextField = ""
    }
  }
};
</script>
<style></style>
