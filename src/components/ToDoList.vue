<script setup lang="ts">
import { ref } from 'vue';

const header = ref('To Do List');
const newTodo = ref("");
const priority = ref(false);
const items = ref([
    { id: 1, text: "Do leetcode problem", isCompleted: true, isHighPriority: true },
    { id: 2, text: "Learn caro kann theory", isCompleted: false, isHighPriority: false },
    { id: 3, text: "Study about backend design patterns", isCompleted: true, isHighPriority: true }
]);

const props = defineProps(['greetings']);
function toggleCompleted(todo) {
    todo.isCompleted = !todo.isCompleted;
}

function deleteTodo(todo) {
    items.value = items.value.filter((item) => item.id !== todo.id);
}

function addTodo() {
    if (newTodo.value.trim() === "") return;

    const newId = items.value.length ? items.value[items.value.length - 1].id + 1 : 1;
    items.value.push({ 
        id: newId, 
        text: newTodo.value, 
        isCompleted: false, 
        isHighPriority: priority.value 
    });

    newTodo.value = "";
    priority.value = false;
}
</script>

<template>
    <h1>{{ greetings }}</h1>
    <h3>{{ header }}</h3>
    <form class="add-item-form" @submit.prevent="addTodo">
        <input v-model="newTodo" placeholder="Add new Todo" type="text">
        <label>
            <input type="checkbox" v-model="priority"> High Priority
        </label>
        <button class="btn btn-primary">Add Item</button>
    </form>
    <ul>
        <li v-for="item in items" :key="item.id">
            <span :class="{ completed: item.isCompleted }" @click="toggleCompleted(item)">
                {{ item.text }} 
                <span v-if="item.isHighPriority"> (High Priority) </span>
            </span> 
            <button @click="deleteTodo(item)" class="btn btn-danger">Delete</button>
        </li>
    </ul>
</template>

<style>
.completed {
    text-decoration: line-through;
}
</style>
