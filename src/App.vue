<!-- src/App.vue -->
<template>
  <ion-app>
    <ion-page>
      <to-do-list :todos="todos"
                  @remove-todo="removeTodo"
                  @start-edit="startUpdate"
                  @save-edit="saveUpdate"
      />
      <add-to-do @add-todo="addTodo" />
    </ion-page>
    <ion-toast
        :is-open="isOpen"
        message="ToDo Added Successfully"
    >
    </ion-toast>
  </ion-app>
</template>

<script>
import { IonApp, IonPage, IonToast } from '@ionic/vue';
import ToDoList from './components/ToDoList.vue';
import AddToDo from "./components/AddToDo.vue";
import { ref } from 'vue';
export default {
  components: {
    AddToDo,
    ToDoList,
    IonApp,
    IonPage,
    IonToast
  },
  setup() {
    const todos = ref([]);
    const isOpen = ref(false);
    const addTodo = (newTodo) => {
      todos.value.push({todo: newTodo, edit: false});
      isOpen.value = true;
      setTimeout(() => {
        isOpen.value = false;
      }, 2000);
    };

    const startUpdate = (index) => {
      todos.value[index].edit = true;
    }

    const saveUpdate = (obj) => {
      todos.value[obj.index].todo = obj.value.todo;
      todos.value[obj.index].edit = false;
    }

    const removeTodo = (index) => {
      todos.value.splice(index, 1);
    };

    return {
      todos,
      addTodo,
      removeTodo,
      startUpdate,
      saveUpdate,
      isOpen
    };
  }
};
</script>
