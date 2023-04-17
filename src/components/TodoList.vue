<template>
  <div>
    <v-card>
      <v-card-title primary-title>
        <v-container>
          <v-row
            class="d-flex flex-row"
            v-for="(item, index) in todos"
            :key="index"
          >
            <v-col cols="12" class="d-flex flex-row align-center">
              <v-checkbox v-model="item.completed"></v-checkbox>
              <span :class="{ strikeout: item.completed }">{{
                item.title
              }}</span>
              <v-spacer></v-spacer>
              <v-btn
                color="primary"
                class="mr-3"
                @click="(dialog = true), curTask(item.title)"
              >
                <v-icon> mdi-note-edit </v-icon>
              </v-btn>
              <v-btn color="error" @click="$emit('onRemove', item.id)">
                <v-icon> mdi-trash-can-outline </v-icon>
              </v-btn>
            </v-col>
            <v-col cols="12">
              <v-divider></v-divider>
            </v-col>
          </v-row>
        </v-container>
      </v-card-title>
    </v-card>
    <v-dialog v-model="dialog" max-width="500">
      <v-card>
        <v-card-title class="primary">
          <v-row>
            <v-col cols="6">
              <span style="color: white">Edit Task</span>
            </v-col>
            <v-col class="d-flex flex justify-end" cols="6">
              <v-btn icon color="white" @click="dialog = false">
                <v-icon>mdi-close</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-card-title>

        <v-container class="pa-5">
          <span>{{ currentTask }}</span>
          <v-text-field
            name="name"
            label="Edit Task"
            id="id"
            v-model="taskTextField"
          ></v-text-field>
        </v-container>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn :disabled="taskTextField.length < 1" color="primary" text @click="editTask()"> I accept </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  name: "TodoList",
  props: ["todos"],
  data() {
    return {
      dialog: false,
      currentTask: "",
      taskTextField: "",
    };
  },
  methods: {
    curTask(task) {
      this.currentTask = task;
    },
    editTask() {
      this.$emit("onEdit", this.taskTextField);
      this.taskTextField = ""
    },
  },
};
</script>
<style scoped>
.strikeout {
  text-decoration: line-through;
}
</style>
