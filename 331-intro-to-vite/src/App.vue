<script setup lang="ts">
import { RouterLink, RouterView, useRouter } from 'vue-router'
import { ref } from 'vue'

const perPage = ref(2)
const router = useRouter()

function updatePerPage(size: number) {
  perPage.value = size
  router.push({ name: 'event-list-view', query: { page: 1, perPage: size } })
}
</script>

<template>
  <div id="layout">
    <header>
      <div class="wrapper">
        <nav>
          <RouterLink :to="{ name: 'event-list-view', query: { page: 1, perPage: perPage }}">Event</RouterLink> |
          <RouterLink :to="{ name: 'about' }">About</RouterLink> |
          <RouterLink :to="{ name: 'student' }">Student</RouterLink>
        </nav>
      </div>
    </header>
    <div class="pagination-controls">
      <button @click="updatePerPage(1)">Show 1 per page</button>
      <button @click="updatePerPage(2)">Show 2 per page</button>
      <button @click="updatePerPage(3)">Show 3 per page</button>
      <button @click="updatePerPage(4)">Show 4 per page</button>
      <button @click="updatePerPage(5)">Show 5 per page</button>
      <button @click="updatePerPage(6)">Show 6 per page</button>
    </div>
    <RouterView :key="$route.fullPath" />
  </div>
</template>

<style>
#layout {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #2c3e50;
}
nav a.router-link-exact-active {
  color: #42b983;
}
.pagination-controls {
  margin: 20px;
}
.pagination-controls button {
  margin: 0 10px;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  background: linear-gradient(145deg, #6ac1ff, #3d8eff);
  color: white;
  font-weight: bold;
  cursor: pointer;
  transition: background 0.3s, transform 0.3s;
  box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
}
.pagination-controls button:hover {
  background: linear-gradient(145deg, #3d8eff, #6ac1ff);
  transform: translateY(-3px);
}
.pagination-controls button:active {
  background: linear-gradient(145deg, #3d8eff, #6ac1ff);
  transform: translateY(1px);
}
</style>
