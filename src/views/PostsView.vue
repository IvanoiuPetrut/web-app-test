<script setup>
import { ref, onMounted } from 'vue'

const posts = ref()

async function fetchPosts() {
  try {
    const response = await fetch(import.meta.env.VITE_POSTS_URL)
    if (!response.ok) {
      throw new Error('Network response was not ok')
    }
    const data = await response.json()
    posts.value = data
  } catch (error) {
    console.error('There has been a problem with your fetch operation:', error)
  }
}

onMounted(() => {
  console.log(import.meta.env.VITE_POSTS_URL)
  fetchPosts()
})
</script>

<template>
  <h1>Posts</h1>
  <main>
    {{ posts }}
  </main>
</template>
