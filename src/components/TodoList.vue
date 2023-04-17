<template>
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
            <span>{{ item.title }}</span>
            <v-spacer></v-spacer>
            <v-btn color="error" @click="$emit('onRemove',item.id)">X</v-btn>
          </v-col>
          <v-col cols="12">
            <v-divider></v-divider>
          </v-col>
        </v-row>
      </v-container>
    </v-card-title>
  </v-card>
</template>
<script>
export default {
  name: "TodoList",
  props: ["todos"],
};
</script>
<style></style>
