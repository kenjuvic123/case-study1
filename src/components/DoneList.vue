<script setup lang="ts">
import WelcomeItem from './DoneList.vue'
import DocumentationIcon from './icons/IconDocumentation.vue'
</script>

<template>
  <WelcomeItem>
    <template #icon>
      <DocumentationIcon />
    </template>
    <template #heading>Done </template>
  </WelcomeItem>
</template>
