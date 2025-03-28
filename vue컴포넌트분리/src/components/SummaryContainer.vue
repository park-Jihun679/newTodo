<script setup>
defineProps({
  activeTodoCount: {
    type: String,
  },
  completedTodoCount: {
    type: String,
  },
})

const emits = defineEmits(['remove-all-completed'])

const removeAllCompleted = () => {
  emits('remove-all-completed')
}
</script>

<template>
  <div class="todo-summary">
    <p>
      <span>미완료 항목</span><span>{{ activeTodoCount }}</span>
    </p>
    <p>
      <span>완료 항목</span><span>{{ completedTodoCount }}</span>
    </p>
    <button @click="removeAllCompleted">완료된 항목 삭제</button>
  </div>
</template>

<style scoped>
.todo-summary {
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: var(--space-m);
}
.todo-summary > p {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 0.75rem;
  display: flex;
  align-items: center;
  gap: var(--space-s);
}
.todo-summary p:nth-of-type(1) span:nth-of-type(1) {
  color: var(--blue-dark);
}
.todo-summary span:nth-of-type(2) {
  background-color: var(--gray300);
  padding: var(--space-s);
  border-radius: var(--space-s);
  font-weight: 900;
}
.todo-summary button {
  background-color: var(--blue-dark);
}
</style>
