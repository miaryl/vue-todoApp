<script setup lang="ts">
import { ref, computed } from 'vue';

interface Todo{
  id: number
  text: string
  completed: boolean
}

type FilterType = "all" | "active" | "completed"

const newTodoText = ref<string>("")
const filter = ref<FilterType>("all")

const todos = ref<Todo[]>([
  {id: 1, text: "sleep", completed: true},
  {id:2, text: "prepare lunch", completed:false}
])

// create new task
const addTodo =(): void =>{
  const text = newTodoText.value.trim()
  if(!text) return

  todos.value.push({
    id: Date.now(),
    text,
    completed:false
  })
  newTodoText.value = ""

}

// delete task

const removeTodo = (id: number): void =>{
  todos.value = todos.value.filter(todo => todo.id != id)
}

const filteredTodos = computed<Todo[]>(() => {
  if(filter.value === "active"){
    return todos.value.filter(t=> !t.completed)
  }
  if (filter.value === "completed"){
    return todos.value.filter(t => t.completed)
  }
  return todos.value
}) 

const remainingCount = computed<number>(() =>{
  return todos.value.filter(t  => !t.completed). length
})
</script>
<template>
  <div class="todo-app">

  </div>
</template>