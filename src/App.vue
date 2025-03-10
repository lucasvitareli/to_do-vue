<script setup>
import { reactive } from 'vue';

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


</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>My tasks</h1>
      <p>
        {{ getPendingTasks().length }} pending tasks
      </p>
    </header>
    <form @submit.prevent="insertNewTask">
      <div class="row d-flex align-items-center">
        <div class="col">
          <input type="text" required class="form-control" placeholder="Type here your task"
          :value="state.taskText"
          @change="event => state.taskText = event.target.value"/>
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Insert</button>
        </div>
        <col class="md-2" >
      </div>
      <select class="form-control d-flex mt-4 text-center" @change="event => state.filter = event.target.value"> 
        <option value="all">All tasks</option>
        <option value="pending">Pending</option>
        <option value="completed">Completed</option>
      </select>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="task in getFilteredTasks()">
        <input type="checkbox" 
        @change="event => task.completed = event.target.checked" 
        :checked="task.completed" :id="task.title"/> 
        <label :class="{done: task.completed }" class="ms-2" :for="task.title">
          {{ task.title }}</label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
