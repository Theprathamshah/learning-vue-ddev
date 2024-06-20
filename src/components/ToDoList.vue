<script setup>
import { ref } from 'vue';

const header = ref('To Do List')
const newTodo = ref("")
const priority = ref(false)
const items = ref([
    { text: "Do leetcode problem", completed: false },
    { text: "Learn caro kann theory", completed: true },
    { text: "Study about backend design patterns", completed: false }
]);

</script>

<template>
    <h1>{{ header }}</h1>
    <form class="add-item-form" @submit.prevent ="items.push({id:items.length,text:newTodo,completed:false,isHighPriority:priority})">

        <input v-model="newTodo"  placeholder="Add new Todo" type="text" >
        <label >
            <input type="checkbox" name="" v-model="priority" id="">
            High Priority
        </label>
        <button class="btn btn-primary" >Add Item</button>
    </form>
    <ul>
        <li v-for="item in items">{{ item.text }}  <span style="color: red"> {{ item.isHighPriority ? 'High Priority' : '' }}</span></li>
    </ul>


</template>