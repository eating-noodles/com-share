<script setup lang="ts">
const hello = () => {
  alert('Hello World')
}
</script>

<template>
  <div>
    <div color-red>Hello World</div>
    <button @click="hello">click</button>
  </div>
</template>
