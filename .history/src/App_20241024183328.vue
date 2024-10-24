<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class=".container">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/guesser">Guesser</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

