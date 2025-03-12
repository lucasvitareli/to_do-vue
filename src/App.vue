<script setup>
  import { reactive } from 'vue';
  import MyHeader from './components/MyHeader.vue';
  import MyForm from './components/MyForm.vue';
  import taskList from './components/taskList.vue';

  const state = reactive({
    tasks: [
      {
        title: 'Study ES6',
        completed: false,
      },
      {
        title: 'Study SASS',
        completed: false,
      },
      {
        title: 'Go to the gym',
        completed: true,
      }
    ],
    
    filter: 'All',
    taskText: '',

  })

  const getPendingTasks = () => {
    return state.tasks.filter(task => !task.completed);
  }

  const getCompletedTasks = () => {
    return state.tasks.filter(task => task.completed);
  }

  const getFilteredTasks = () => {
    const {filter} = state;

    switch (filter) {
      case 'pending':
        return getPendingTasks();
      case 'completed':
        return getCompletedTasks();
      default:
        return state.tasks;
    }
  }

  const insertNewTask = () => {
    const newTask = {
      title: state.taskText,
      completed: false,
    }
    state.tasks.push(newTask);
    state.taskText = '';
  }

  const getPendingTasksCount = () => {
    return state.tasks.filter(task => !task.completed).length;
  }

  const toggleTaskCompletion = (task) => {
    task.completed = !task.completed;
  }

</script>

<template>
  <div class="container">
    <MyHeader :pending-tasks="getPendingTasksCount()" />
    <MyForm :change-filter="event => state.filter = event.target.value" 
      :temp-task="state.taskText" :edit-temp-task="event => state.taskText = event.target.value" 
      :insert-new-task="insertNewTask"/>
    <taskList :tasks="getFilteredTasks()" @toggle-task="toggleTaskCompletion" /> 
  </div>
</template>


