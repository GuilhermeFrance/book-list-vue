<script setup>
import { reactive, ref } from "vue";
import { watch } from "vue";
import Books from "./components/Books.vue";
import BookProgress from "./components/BookProgress.vue";
import AddBook from './components/AddBook.vue'

let showAddContainer = ref(false)




let books = reactive(loadBooks().length ? loadBooks() :([
  {
    id: 1,
    title: "Nunca é hora de parar",
    cover:
      "/images/book6.jpg",
    isRead: true,
    status: 'Não lido',
    isbn: "0-395-07157-8",
    author: "David Goggins",
  },
  {
    id: 2,
    title: "It - A Coisa",
    cover:
      "/images/book8.jpg",
    isRead: false,
    status: 'Não lido',
    isbn: "0-395-07157-8",
    author: "Stephen King",
  },
  {
    id: 3,
    title: "Nada pode me ferir",
    cover:
      "/images/book5.jpg",
    isRead: false,
    status: 'Não lido',
    isbn: "0-395-07157-8",
    author: "David Goggins",
  },
  {
    id: 4,
    title: "Algorítimos e Lógica de Programação",
    cover:
      "/images/book9.jpg",
    isRead: false,
    status: 'Não lido',
    isbn: "0-395-07157-8",
    author: "Marco A. Furlan",
  },
   {
    id: 5,
    title: "A arte da Guerra",
    cover:
      "/images/book10.jpg",
    isRead: false,
    status: 'Não lido',
    isbn: "0-395-07157-8",
    author: "Sun Tzu",
  }
]));

watch(
  books,
  (newVal) => {
    localStorage.setItem("books", JSON.stringify(newVal));
  },
  { deep: true } // precisa para observar mudanças dentro do array/objetos
);

function addBook(newBook){
  newBook.id = Math.max(...books.map(el => el.id)) + 1;
  books.push(newBook)
  showAddContainer.value = false; 
  console.log(books)
}

function loadBooks() {
  const saved = localStorage.getItem("books");
  if (saved) {
    try {
      return JSON.parse(saved);
    } catch {
      return [];
    }
  }
  return [];
}

const status = ref(books.status ?? false)

const order = ['Lido', 'Não lido', 'Lendo']


function toggleStatus(id) {
  const book = books.find(b => b.id === id);
  if (!book) return;
  const currentIndex = order.indexOf(book.status);
  const nextIndex = (currentIndex + 1) % order.length;
  book.status = order[nextIndex];
  // manter isRead em sincronia
  book.isRead = book.status === 'Lido';
  // se quiser persistir: API / localStorage aqui
  console.log(`Livro ${book.id} agora:`, book.status);
}

function toggleIsRead(id) {
  const book = books.find(b => b.id === id);
  if (!book) return;
  book.isRead = !book.isRead;
  book.status = book.isRead ? 'Lido' : 'Não lido';
}
</script>

<template>
  <div v-if="!showAddContainer" class="container">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button @click="showAddContainer = !showAddContainer" class="btn" disabled>Adicionar Livro +</button>
    </div>

    <div class="books-container">
      <Books @toggleIsRead="toggleIsRead" @toggleStatus="toggleStatus" :books="books" />
      <BookProgress :books="books" />
    </div>
  </div>
  <div v-else class="container">
    <AddBook @addBook="addBook" @closeAddBook="showAddContainer = false" />
  </div>
</template>

<style scoped></style>
