<script setup>
defineProps({
  title: {
    type: String,
    required: true,
  },
})
</script>

<template>
  <div>
    <header class="hd">
      <h1>TodoList</h1>
    </header>
  </div>
</template>

<style scoped>
.hd {
  background-color: var(--gray700);
  padding: var(--space-l) 0 calc(var(--space-l) * 1.8);
  text-align: center;
}
.hd h1 {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 2rem;
  font-weight: 500;
}
</style>
