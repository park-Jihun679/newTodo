<script setup>
defineProps({
  filter,
})
const filterOptions = ['all', 'active', 'completed']

const emits = defineEmits(['change-filter'])

const changeFilter = () => {
  emits('change-filter', filter)
}
</script>

<template>
  <div class="filter-container">
    <button
      v-for="(option, index) in filterOptions"
      :key="index"
      :class="filter === option ? 'active' : ''"
      @click="changeFilter"
    >
      {{ option === 'all' ? '전체' : option === 'active' ? '미완료' : '완료' }}
    </button>
  </div>
</template>

<style scoped>
.filter-container {
  display: flex;
  gap: var(--space-m);
}
</style>
