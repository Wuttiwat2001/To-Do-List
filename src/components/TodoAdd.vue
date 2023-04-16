<template>
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
</template>
<script>
export default {
  name: "TodoAdd",
  data(){
    return{
      taskTextField: "",
    }
  },
  methods:{
    addTask(){
      this.$emit("onSubmit", this.taskTextField)
      this.taskTextField = ""
    }
  }
};
</script>
<style></style>
