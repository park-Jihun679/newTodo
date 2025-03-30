<script setup>
import { ref } from 'vue'
const emits = defineEmits(['change-filter'])
const props = defineProps({
  filterOption: String,
})
const filterOptions = ['all', 'active', 'completed']

const changeFilter = (option) => {
  emits('change-filter', option)
}
</script>

<template>
  <div class="filter-container">
    <button
      v-for="(option, index) in filterOptions"
      :key="index"
      :class="filterOption === option ? 'active' : ''"
      @click="changeFilter(option)"
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
