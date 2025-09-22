<script setup>
import { reactive, ref } from "vue";
import Books from "./components/Books.vue";
import BookProgress from "./components/BookProgress.vue";
import AddBook from './components/AddBook.vue'

let showAddContainer = ref(false)




let books = reactive([
  {
    id: 1,
    title: "History of Europe",
    cover:
      "/images/book1.jpg",
    isRead: true,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
  {
    id: 2,
    title: "Penguin Classics",
    cover:
      "/images/book2.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo, Jon Snow",
  },
  {
    id: 3,
    title: "Becoming",
    cover:
      "/images/book3.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
  {
    id: 4,
    title: "Sonnets",
    cover:
      "/images/book4.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
]);

function addBook(newBook){
  newBook.id = Math.max(...books.map(el => el.id)) + 1;
  books.push(newBook)
  showAddContainer.value = false; 
  console.log(books)
}


function toggleIsRead(id) {
  books.forEach(book => {
    if (book.id === id) {
      book.isRead = !book.isRead
    }
  });
}
</script>

<template>
  <div v-if="!showAddContainer" class="container">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button @click="showAddContainer = !showAddContainer" class="btn">Adicionar Livro +</button>
    </div>

    <div class="books-container">
      <Books @toggleIsRead="toggleIsRead" :books="books" />
      <BookProgress :books="books" />
    </div>
  </div>
  <div v-else class="container">
    <AddBook @addBook="addBook" @closeAddBook="showAddContainer = false" />
  </div>
</template>

<style scoped></style>
