<!-- src/components/ToDoList.vue -->
<template>
  <div>
    <h1>ToDo List</h1>
    <ion-list>
      <ion-item v-for="(todo, index) in todos" :key="index">
        <ion-label v-if="!todo.edit">{{ todo.todo }}</ion-label>
        <ion-input v-if="todo.edit" v-model="editTodo.todo" @keyup.enter="saveUpdate(index)" placeholder="Update Todo" />
        <ion-button v-if="!todo.edit" @click="updateToDo(index)">Edit</ion-button>
        <ion-button color="success" v-if="todo.edit" @click="saveUpdate(index)">Save</ion-button>
        <ion-button color="danger" @click="removeTodo(index)">Remove</ion-button>
      </ion-item>
    </ion-list>
  </div>
</template>

<script>
import { IonButton, IonList, IonItem, IonLabel, IonInput } from "@ionic/vue";

export default {
  components: {
    IonButton,
    IonList,
    IonItem,
    IonLabel,
    IonInput
  },
  props: {
    todos: Array, // Define a prop called "todos" as an array
  },
  methods: {
    removeTodo(index) {
      this.$emit('remove-todo', index); // Emit a custom event to remove a ToDo
    },
    updateToDo(index) {
      this.editTodo = this.todos[index];
      this.$emit('start-edit', index);
    },
    saveUpdate(index) {
      this.$emit('save-edit', {index: index, value: this.editTodo});
      this.editTodo = null;
    }
  },
  data() {
    return {
      editTodo: null
    }
  }
};
</script>