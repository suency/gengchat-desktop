<script setup lang="ts">
import ChatGpt from './components/ChatGpt.vue'

console.log("[App.vue]", `Hello world from Electron ${process.versions.electron}!`)
</script>

<template>
  <div>
    <ChatGpt msg="GengChat"></ChatGpt>
  </div>
</template>

<style>
</style>
