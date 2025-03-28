<script setup>
import { ref, onMounted, computed } from 'vue'
import FilterContainer from './components/FilterContainer.vue'
import HeaderLayout from './components/HeaderLayout.vue'
import InputContainer from './components/InputContainer.vue'
import SummaryContainer from './components/SummaryContainer.vue'
import TodoItem from './components/TodoItem.vue'

onMounted(() => {
  loadTodos()
})

const todos = ref([])
const filterOption = ref('')

const addTodo = (text) => {
  todos.value.push({
    id: Date.now(),
    text: text,
    completed: false,
    createdAt: formatDate(new Date()),
  })
}

const toggleCompleted = (id) => {
  const todo = todos.value.find((todo) => todo.item === id)
  todo.completed = !todo.completed
}

const changeFilter = (filter) => {
  filterOption.value = filter
}

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id)
}

const removeAllCompleted = () => {
  todos.value = todos.value.filter((todo) => !todo.completed)
  saveTodos()
}

// localstrage 에 저장
const saveTodos = () => {
  localStorage.setItem('todos', JSON.stringify(todos.value))
}

// localstrage 에서 호출하는 함수
const loadTodos = () => {
  let list = localStorage.getItem('todos')
  list ? (todos.value = JSON.parse(list)) : []
}

const activeTodoCount = computed(() => {
  return todos.value.filter((todo) => !todo.completed).length
})
const completedTodoCount = computed(() => {
  return todos.value.filter((todo) => todo.completed).length
})

const filteredTodos = computed(() => {
  if (filterOption.value == 'active') {
    return todos.value.filter((todo) => !todo.completed)
  } else if (filterOption.value == 'completed') {
    return todos.value.filter((todo) => todo.completed)
  } else {
    return todos.value
  }
})

// 날짜 포멧
const formatDate = (date) => {
  const pad = (num) => String(num).padStart(2, '0')
  return `${pad(date.getMonth() + 1)}/${pad(date.getDate())} ${pad(
    date.getHours(),
  )}:${pad(date.getMinutes())}:${pad(date.getSeconds())}`
}
</script>

<template>
  <HeaderLayout :title="TODO" />
  <InputContainer @add-todo="addTodo" />
  <FilterContainer @change-filter="changeFilter" />
  <ul class="todo-list">
    <TodoItem
      v-for="todo in filteredTodos"
      :key="todo.id"
      :todo="todo"
      @toggle-completed="toggleCompleted"
    />
  </ul>
  <SummaryContainer @remove-all-completed="removeAllCompleted" :activeTodoCount="activeTodoCount" :completedTodoCount="completedTodoCount" />
</template>

<style scoped></style>
