<template>
  <header>
    <nav>
      <ul>
        <li>
          <NuxtLink to="/" exact active-class="active-link"
            >Weighted String</NuxtLink
          >
        </li>
        <li>
          <NuxtLink to="/soal-2" active-class="active-link"
            >Highest Palindrome</NuxtLink
          >
        </li>
        <li>
          <NuxtLink to="/soal-3" active-class="active-link"
            >Balanced Bracked</NuxtLink
          >
        </li>
      </ul>
    </nav>
  </header>
</template>

<script setup>
import { ref } from "vue";
const menuItems = ref([
  { title: "Menu 1" },
  { title: "Menu 2" },
  { title: "Menu 3" },
]);
</script>

<style scoped>
.active-link {
  font-weight: bold;
}
header {
  padding: 20px;
  background: #3778f3;
}

nav ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  justify-content: center;
}

nav ul li {
  margin-right: 20px;
}

nav ul li:last-child {
  margin-right: 0;
}

nav ul li a {
  text-decoration: none;
  color: white;
}
</style>
