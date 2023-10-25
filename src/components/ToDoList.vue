<!-- src/components/ToDoList.vue -->
<template>
  <div>
    <h1>ToDo List</h1>
    <ion-list>
      <ion-item v-for="(todo, index) in todos" :key="index">
        <ion-label>{{ todo }}</ion-label>
        <ion-button @click="removeTodo(index)">Remove</ion-button>
      </ion-item>
    </ion-list>
  </div>
</template>

<script>
import { IonButton, IonList, IonItem, IonLabel } from "@ionic/vue";

export default {
  components: {
    IonButton,
    IonList,
    IonItem,
    IonLabel
  },
  props: {
    todos: Array, // Define a prop called "todos" as an array
  },
  methods: {
    removeTodo(index) {
      this.$emit('remove-todo', index); // Emit a custom event to remove a ToDo
    },
  },
  setup(props) {
    console.log(props.todos)
  }
};
</script>