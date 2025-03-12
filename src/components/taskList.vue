<script setup>
const props = defineProps(['tasks']);
const emit = defineEmits(['toggle-task']);
</script>

<template>
    <ul class="list-group mt-4">
        <li v-for="task in props.tasks" :key="task.title" class="list-group-item">
            <input type="checkbox" :checked="task.completed" @change="emit('toggle-task', task)" />
            <label :class="{ 'done': task.completed }" class="ms-2">{{ task.title }}</label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>