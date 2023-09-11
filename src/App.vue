<script setup lang="ts">
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
import { ref } from 'vue'

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { 
    id: id++, 
    text: '澆花餵魚裝水', 
    done: true 
  },
  { 
    id: id++, 
    text: '帶手機鑰匙錢包充電器雨衣', 
    done: false 
  },
])
const textCenter = ref('textCenter')
const justifyContentCenter = ref('justifyContentCenter')

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <h1 :class="textCenter">出門檢查清單</h1>
    <div :class="justifyContentCenter">
      <div>
        <button>新增代辦事項</button><br>
        <input v-model="newTodo"><br>
      </div>
      <div>
        <ul>
          <li v-for="todo in todos" :key="todo.id">
            <input type="checkbox" v-model="todo.done">
            <span :class="{ done: todo.done }">{{ todo.text }}</span>
            <button @click="removeTodo(todo)">刪除</button>
          </li>
        </ul>
        <button @click="hideCompleted = !hideCompleted">
          {{ hideCompleted ? '顯示全部' : '隱藏已完成事項' }}
        </button>
      </div>
    </div>
  </form>
</template>

<style scoped>
  form {
    background-color: lightskyblue;
    border-radius: 10px;
    padding: 20px;
  }
  ul {
    list-style-type: none;
  }
  li {
    padding: 10px;
  }

  .textCenter {
    text-align: center;
  }
  .justifyContentCenter {
    display: flex;
    justify-content: center;
    padding: 20px;
  }
  .done {
    text-decoration: line-through;
  }
</style>
