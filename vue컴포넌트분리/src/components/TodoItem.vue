<script setup>
const props = defineProps({
  todo: {
    type: Object,
    require: true,
  },
})

const emits = defineEmits(['toggle-completed'])
</script>

<template>
  <!-- <li class="empty" v-if="todos.length === 0">
    <i class="fa fa-paper-plane" aria-hidden="true"></i>
    <p>할 일을 입력해 주세요</p>
  </li> -->
  <li :class="{ completed: todo.completed }" @click="emits('toggle-completed', todo.id)">
    <input type="checkbox" />
    <span>{{ todo.text }}</span>
    <time>{{ todo.createdAt }}</time>
    <i class="fa fa-trash" @click.stop=""></i>
  </li>
</template>

<style scoped>
.todo-list {
  margin: var(--space-l) auto;
}
.todo-list li {
  display: flex;
  align-items: center;
  gap: var(--space-s);
  padding: var(--space-s);
  border-bottom: dotted 1px var(--gray200);
  cursor: pointer;
  transition: 0.3s;
}
.todo-list li:hover {
  background-color: var(--gray500);
}
.todo-list li.completed {
  opacity: 0.1;
}
.todo-list li.completed span {
  text-decoration: line-through;
}
.todo-list span {
  flex: 1;
}
.todo-list time {
  font-size: 0.75rem;
}
.todo-list i {
  border: 1px solid transparent;
  padding: var(--space-s);
  color: var(--gray100);
  border-radius: var(--space-s);
  transition: 0.3s;
}
.todo-list i:hover {
  border: 1px solid var(--danger);
  color: var(--danger);
}
li .empty {
  flex-direction: column;
  padding: var(--space-l) 0;
}
li .empty:hover {
  background-color: transparent !important;
}
li .empty i {
  font-size: 3rem;
}
li .empty i:hover {
  border: none;
  color: var(--gray200);
}
</style>
