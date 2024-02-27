<script setup>
import { ref } from 'vue';

const tasks = ref([
    { name: 'Task 1', time: 30 },
    { name: 'Task 2', time: 40 },
    { name: 'Task 3', time: 60 },
    { name: 'Task 4', time: 45 },
    { name: 'Task 5', time: 50 }
]);
const editedTask = ref(null);
const showEditPopup = ref(false);

const editTask = (index) => {
    editedTask.value = { ...tasks.value[index] };
    showEditPopup.value = true;
};

const updateTask = () => {
    const index = tasks.value.indexOf(editedTask.value);
    tasks.value.splice(index, 1, { ...editedTask.value });
    // Move the edited task to the beginning of the tasks array
    tasks.value.unshift(tasks.value.splice(index, 1)[0]);
    showEditPopup.value = false;
};
const cancelEdit = () => {
    showEditPopup.value = false;
};
</script>


<template>
    <div id="app" class="bg-green-100 min-h-screen flex flex-col items-center justify-center">
        <div class="max-w-lg w-full bg-green-300 rounded shadow-md p-6">
            <h1 class="text-2xl font-bold mb-4">Task Manager</h1>
            <ul>
                <li v-for="(task, index) in tasks" :key="index"
                    class="flex justify-between items-center border-b border-gray-200 py-4">
                    <div>
                        <span class="font-semibold">{{ task.name }}</span>
                        <span class="text-gray-500"> - {{ task.time }} minutes</span>
                    </div>
                    <button @click="editTask(index)"
                        class="text-sm text-white bg-green-500 hover:bg-green-600 px-4 py-2 ml-5 rounded-lg">Edit</button>
                </li>
            </ul>
        </div>
        <div v-if="showEditPopup"
            class="fixed top-0 left-0 w-full h-full flex items-center justify-center bg-gray-800 bg-opacity-50">
            <div class="popup max-w-lg w-full bg-green-200 rounded shadow-md p-6">
                <h2 class="text-lg font-bold mb-4">Edit Task</h2>
                <form @submit.prevent="updateTask" class="space-y-4">
                    <div>
                        <label for="edit-name" class="block text-sm font-semibold">Name:</label>
                        <input type="text" id="edit-name" v-model="editedTask.name" required
                            class="border border-gray-300 rounded w-full px-3 py-2">
                    </div>
                    <div>
                        <label for="edit-time" class="block text-sm font-semibold">Time:</label>
                        <input type="number" id="edit-time" v-model.number="editedTask.time" required
                            class="border border-gray-300 rounded w-full px-3 py-2">
                    </div>
                    <div class="flex justify-end mt-8">
                        <button type="submit"
                            class="text-sm text-white bg-green-500 hover:bg-green-600 px-4 py-2 ml-5 rounded-lg">Update</button>
                            <button type="button" @click="cancelEdit"
                                class="text-sm text-white bg-green-500 hover:bg-green-600 px-4 py-2  rounded-lg ml-6">Cancel</button>
                    </div>
                </form>
            </div>
        </div>
    </div>
</template>


<style>.popup {
    width: 320px;
}</style>
