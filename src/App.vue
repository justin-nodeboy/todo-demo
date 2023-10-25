<!-- src/App.vue -->
<template>
  <ion-app>
    <to-do-list :todos="todos" @remove-todo="removeTodo" />
    <add-to-do @add-todo="addTodo" />
  </ion-app>
</template>

<script>
import { IonApp } from '@ionic/vue';
import ToDoList from './components/ToDoList.vue';
import AddToDo from "./components/AddToDo.vue";
import { ref } from 'vue';
export default {
  components: {
    AddToDo,
    ToDoList,
    IonApp
  },
  setup() {
    const todos = ref([]);
    const addTodo = (newTodo) => {
      todos.value.push(newTodo);
    };

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      addTodo,
      removeTodo,
    };
  }
};
</script>
