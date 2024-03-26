<template>
  <div>
    <WelcomeItem>
      <template #icon>
        <DocumentationIcon />
      </template>
      <div class="title">Task List Details:</div>

      <template #heading> </template>
    </WelcomeItem>
  </div>
</template>

<script setup lang="ts">
import WelcomeItem from '../components/WelcomeItem.vue'
</script>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}

.title {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}
</style>
