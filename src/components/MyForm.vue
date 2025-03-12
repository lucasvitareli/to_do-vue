<script setup>
const props = defineProps(['insertNewTask', 'tempTask', 'changeFilter', 'editTempTask']);
</script>

<template>
    <form @submit.prevent="props.insertNewTask">
        <div class="row d-flex align-items-center">
            <div class="col">
                <input type="text" required class="form-control" placeholder="Type here your task"
                    :value="props.tempTask" @change="props.editTempTask" />
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Insert</button>
            </div>
            <col class="md-2">
        </div>
        <select class="form-control d-flex mt-4 text-center" @change="props.changeFilter">
            <option value="all">All tasks</option>
            <option value="pending">Pending</option>
            <option value="completed">Completed</option>
        </select>
    </form>
</template>