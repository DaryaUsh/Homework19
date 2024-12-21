<template>
  <div id="app" class="app-container">

    <h1 class="app-title">To-Do list Vue3</h1>

    <TodoList 
      :tasks="tasks" 
      @add-task="addTask" 
      @remove-task="removeTask" 
      @toggle-completion="toggleTaskCompletion"
    />
  </div>
</template>

<script>
import { ref } from 'vue';
import TodoList from './components/TodoList.vue';

export default {
  name: 'App',
  components: { TodoList },
  setup() {

    const tasks = ref([]);

    const addTask = (newTask) => {
      tasks.value.push({
        id: Date.now(), 
        text: newTask, 
        completed: false 
      });
    };

    const removeTask = (taskId) => {
      tasks.value = tasks.value.filter(task => task.id !== taskId);
    };

    const toggleTaskCompletion = (task) => {
      task.completed = !task.completed;
    };

    return { tasks, addTask, removeTask, toggleTaskCompletion };
  }
};
</script>

<style scoped>
/* Стили для главного контейнера приложения */
.app-container {
  font-family: Arial, sans-serif;
  text-align: center;
  background-color: #f2c88b;
  padding: 20px;
  border-radius: 10px;
  max-width: 600px;
  margin: 40px auto;
  box-shadow: 0 4px 8px #35424e;
}

.app-title {
  font-size: 2.5rem;
  color: #35424e;
  margin-bottom: 20px;
}
</style>