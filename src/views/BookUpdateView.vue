<template>
  Book {{ mode }}
    <div>name: <input type="text" v-model="bookData.name"></div>
    <div>author: <input type="text" v-model="bookData.author"></div>
    <button @click="addOrUpdateBook">{{ mode }} book</button>
</template>

<script setup>
import { ref, reactive, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router';
import { useBookStore } from '../stores/book';

const route = useRoute()
const router = useRouter()
const bookStore = useBookStore()
const bookData = reactive({
    name: '',
    author: ''
})
const mode = ref('')
const bookIndex = ref(-1)


const addOrUpdateBook = () => {
    if(mode.value === 'create') {
        bookStore.addBook(bookData)
    } else {
        bookStore.updateBook(bookData, bookIndex.value)
    }
    router.push({ name: 'book-list' })
}

onMounted(() => {
    if (route.params.id) {
    bookIndex.value = parseInt(route.params.id)
    const cBookData = bookStore.books[bookIndex.value]
    bookData.name = cBookData.name
    bookData.author = cBookData.author
  }
    if(route.name === 'book-create') {
        mode.value = 'create'
    } else {
        mode.value = 'update'
    }
})

</script>

<style>

</style>