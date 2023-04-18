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
                @click="(dialog = true), curTask(item.title, item.id)"
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
              <v-btn icon color="white" @click="closeDialog">
                <v-icon>mdi-close</v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </v-card-title>

        <v-container class="pa-5">
          <span>{{ currentTask }}</span>
          <v-text-field
            name="task"
            label="Edit Task"
            id="task"
            v-model="taskTextField"
          />
        </v-container>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
            :disabled="taskTextField.length < 1"
            color="primary"
            text
            @click="editTask()"
          >
            I accept
          </v-btn>
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
      id: "",
    };
  },
  methods: {
    curTask(task, id) {
      this.currentTask = task;
      this.id = id;
    },
    editTask() {
      const task = {
        id: this.id,
        title: this.taskTextField,
      };
      this.$emit("onEdit", task);
      this.currentTask = "";
      this.taskTextField = "";
      this.id = "";
      this.dialog = false;
    },
    closeDialog() {
      this.dialog = false;
      this.currentTask = "";
      this.taskTextField = "";
      this.id = "";
    },
  },
};
</script>
<style scoped>
.strikeout {
  text-decoration: line-through;
}
</style>
