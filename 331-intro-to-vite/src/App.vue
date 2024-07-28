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
          <RouterLink :to="{ name: 'event-list-view', query: { page: 1, perPage: perPage.value }}">Event</RouterLink> |
          <RouterLink :to="{ name: 'about' }">About</RouterLink> |
          <RouterLink :to="{ name: 'student' }">Student</RouterLink>
        </nav>
      </div>
    </header>
    <div class="pagination-controls">
      <button @click="updatePerPage(2)">Show 2 per page</button>
      <button @click="updatePerPage(5)">Show 5 per page</button>
      <button @click="updatePerPage(10)">Show 10 per page</button>
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
}
</style>
