<script setup>
import { ref } from 'vue';

const header = ref('To Do List')
const newTodo = ref("")
const priority = ref(false)
const items = ref([
    { id: 1, text: "Do leetcode problem", isCompleted: true, isHighPriority: true },
    { id: 2, text: "Learn caro kann theory", isCompleted: false, isHighPriority: false },
    { id: 3, text: "Study about backend design patterns", isCompleted: true, isHighPriority: true }
]);


function toggleCompleted(todo) {
    todo.isCompleted = !todo.isCompleted;
}

function deleteTodo(todo) {
    items.value = items.value.filter((item) => item.id !== todo.id);
}

</script>

<template>
    <h1>{{ header }}</h1>
    <div class="add-item-form">

        <input v-model="newTodo"
            v-on:keyup.enter="items.push({ text: newTodo, isCompleted: false, isHighPriority: false, id: items.length + 1 })"
            placeholder="Add new Todo" type="text">
        <label>
            <input type="checkbox" name="" v-model="priority" id="">
            High Priority
        </label>
        <button class="btn btn-primary"
            v-on:click="items.push({ text: newTodo, isCompleted: false, isHighPriority: false, id: items.length + 1 })">Add
            Item</button>
    </div>
    <ul>
        <li v-for="item in items"  >
            <span :class="{ completed: item.isCompleted }" @click="toggleCompleted(item)">{{ item.text }} </span> 
            <button style="color: red"  @click="deleteTodo(item)">Delete</button>
        </li>
    </ul>


</template>

<style>
.completed {
    text-decoration: line-through;
}
</style>