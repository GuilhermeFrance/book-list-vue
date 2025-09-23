<script setup>
const props = defineProps(["books"]);
</script>

<template>
  <div>
    <div class="books-list">
      <div v-for="book in books" :key="book.isbn" class="book">
        <div class="readIt" v-if="book.isRead">
             <i class="fa-solid fa-check"></i>
        </div>
        <div class="readingg" v-if="book.status === 'Lendo'">
             <i class="fa-solid fa-eye"></i>
        </div>
        <div class="book-cover">
          <img :src="book.cover" />

          <button @click="$emit('toggleStatus', book.id)" :class="{isRead : book.status === 'Lido', reading: book.status === 'Lendo', unread: book.status === 'Não lido'}" class="status-btn">
            <i class="fa-solid fa-eye"></i>
            <span>{{ book.status}}</span>
          </button>
        </div>
        <div class="book-details">
          <p class="book-author">{{ book.author }}</p>
          <h3 class="book-title">{{ book.title }}</h3>
          <p class="isbn"><i class="fa-solid fa-hashtag icon"></i> {{ book.isbn }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
