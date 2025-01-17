<script setup>
import Books from "./components/Books.vue";
import BookProgress from "./components/BookProgress.vue";
import AddBook from "./components/AddBook.vue";
import { reactive, ref } from "vue";

let books = reactive([
  {
    id: 1,
    title: "History of Europe",
    cover: "/src/assets/1.jpg",
    isRead: true,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
  {
    id: 2,
    title: "Penguin Classics",
    cover: "/src/assets/2.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo, Jon Snow",
  },
  {
    id: 3,
    title: "Becoming",
    cover: "/src/assets/3.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
  {
    id: 4,
    title: "Sonnets",
    cover: "/src/assets/4.jpg",
    isRead: false,
    isbn: "0-395-07157-8",
    author: "Daniel Trejo",
  },
]);

function addBook(newBook) {
  newBook.id = Math.max(...books.map((el) => el.id)) + 1;
  books.push(newBook);
  showAddBook.value = false;
}

let showAddBook = ref(false);

function toggleIsRead(id) {
  books.forEach((book) => {
    if (book.id === id) {
      book.isRead = !book.isRead;
    }
  });
}
</script>

<template>
  <div v-if="!showAddBook" class="container">
    <h1>📖 Meus Livros</h1>
    <div class="header-btns">
      <button class="btn" @click="showAddBook = true">Adicionar Livro +</button>
    </div>

    <div class="books-container">
      <Books @toggleIsRead="toggleIsRead" :books="books" />

      <BookProgress :books="books" />
    </div>
  </div>
  <div v-else class="container">
    <AddBook @addBook="addBook" @closeAddBook="showAddBook = false" />
  </div>
</template>
