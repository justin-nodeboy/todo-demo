<!-- src/components/AddTodo.vue -->
<template>
  <div>
    <h2>Add ToDo</h2>
    <ion-input v-model="newTodo" @keyup.enter="addTodo" placeholder="Enter a new ToDo" />
    <ion-button @click="addTodo">Add</ion-button>
  </div>
</template>

<script>
import { ref } from 'vue';
import { IonButton, IonInput } from "@ionic/vue";

export default {
  emits: ['add-todo'],
  components: {
    IonButton,
    IonInput
  },
  setup(_, ctx) {
    const newTodo = ref('');

    const addTodo = () => {
      if (newTodo.value.trim() === '') return;

      // Emit a custom event to add a new ToDo
      // Pass the newToDo as the payload
      console.log(newTodo.value)
      ctx.emit('add-todo', newTodo.value);
      newTodo.value = '';
    };

    return {
      newTodo,
      addTodo
    };
  },
};
</script>