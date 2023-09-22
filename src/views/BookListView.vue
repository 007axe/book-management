<template>
  Book List
  <router-link :to="{ name: 'book-create'}"> 
    <button>Add Book</button>
</router-link>
    <div>
        <ul>
            <li v-for="(book, index) in bookStore.books" :key="book">
                {{ index }} {{ book.name }} {{ book.author }}
                <router-link :to="{ name: 'book-update', params: { id: index } }">
                    <button>Edit</button>
                </router-link>
                <button @click="bookStore.removeBook">Delete</button>
            </li>
        </ul>
    </div>

</template>

<script setup>
import { useRouter, RouterLink } from 'vue-router'
import { useBookStore } from '../stores/book.js'

const router = useRouter()
const bookStore = useBookStore()


</script>

<style>

</style>