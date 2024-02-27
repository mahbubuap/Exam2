<script setup>
import { ref } from 'vue';

const name = ref('');
const time = ref(0);
const itemList = ref([]);

const handleSubmit = () => {
    if (name.value.trim() && time.value > 0) {
        itemList.value.push({ name: name.value, time: time.value });
        name.value = '';
        time.value = 0;
    } else {
        alert('Please fill in all fields with valid data.');
    }
};

const removeItem = (index) => {
    itemList.value.splice(index, 1);
};
</script>


<template>
    <div class="container mx-auto p-4  bg-green-100">
        <h2 class="text-3xl font-bold mb-6 text-center">Form</h2>
        <form @submit.prevent="handleSubmit" class="mb-8 bg-green-200 shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <div class="mb-4">
                <label for="name" class="block text-sm font-semibold mb-2">Name:</label>
                <input id="name" type="text" v-model="name"
                    class="appearance-none border rounded-md w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>

            <div class="mb-6">
                <label for="time" class="block text-sm font-semibold mb-2">Time:</label>
                <input id="time" type="number" v-model.number="time"
                    class="appearance-none border rounded-md w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
            </div>

            <button type="submit"
                class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline">Submit</button>
        </form>

        <h2 class="text-3xl font-bold mb-6 text-center">Reactive List</h2>
        <ul class="bg-green-300 shadow-md rounded px-8 pt-6 pb-8 mb-4">
            <li v-for="(item, index) in itemList" :key="index" class="mb-4 flex items-center justify-between border-b pb-4">
                <div>
                    <span class="font-semibold">{{ item.name }}</span> - <span>{{ item.time }}</span>
                </div>
                <button @click="removeItem(index)" class="text-red-500 hover:text-red-700 focus:outline-none ml-7">
                    <svg class="h-5 w-5" fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        viewBox="0 0 24 24" stroke="currentColor">
                        <path d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </li>
        </ul>
    </div>
</template>


<style scoped>
button {
    transition: all 0.3s ease;
}

button:hover {
    opacity: 0.8;
}</style>
