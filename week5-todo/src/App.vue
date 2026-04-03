<script setup>
import { ref } from 'vue';

const newTodo = ref('');

const todos = ref([
  {id: 1, text: 'Vue.js 컴포넌트 복습', done:false},
  {id: 2, text: 'UI/UX 기획안 작성', done:true},
  {id: 3, text: '알고리즘 문제 풀이', done:false},
])

let nextId=4;

const addTodo = () =>{
  if(newTodo.value==='') return;

  todos.value.push({
    id:nextId++,
    text:newTodo.value,
    done:false
  })
  newTodo.value='';
}

const removeTodo = (targetId) => {
  todos.value = todos.value.filter(todo => todo.id !== targetId);
}
</script>

<template>
  <div class="todo-container">
    <h1>To-Do List</h1>
  
  </div>
  <div class="input-area">
    <input type="text"
    v-model.trim="newTodo"
    @keyup.enter="addTodo"
    placeholder="새로운 할 일을 입력 후 Enter">
    <button @click="addTodo">추가</button>
  </div>
  <ul class="todo-list">
    <li v-for="todo in todos" :key="todo.id" class="todo-item">
      <input type="checkbox" v-model="todo.done" class="checkbox">
      <span :class="{ completed: todo.done }" class="text">
        {{ todo.text }}
      </span>
      <button class="delete-btn" @click="removeTodo(todo.id)">삭제</button>
    </li>
  </ul>
</template>

<style scoped>
.todo-container { 
  max-width: 500px; margin: 50px auto; 
  padding: 30px; background: #fff;
  border-radius: 12px; box-shadow: 0 8px 20px rgba(0,0,0,0.1); 
  font-family: sans-serif;
}
h1 {text-align: center; color: #333; margin-bottom: 25px;}
.input-area {display: flex; gap: 10px; margin-bottom: 25px;}
.todo-list {list-style: none; padding: 0; margin: 0;}

.todo-item{
  display: flex; align-items: center; justify-content: space-between;
  padding: 15px; border-bottom: 1px solid #eee; transition: all;
  background-color: 0.2s;
}
.todo-item:hover {background: #f9f9f9;}
.text { font-size: 16px; color: #333; flex: 1; margin-left: 15px;}
.delete-btn {
  background: #e53935; color: white; border: none; padding: 8px 12px;
  border-radius: 6px; cursor: pointer; font-weight: bold;
}

.input-area input{ flex: 1; padding: 12px; border: 1px solid #ddd; 
border-radius: 6px; font-size: 16px; outline: none;}
.input-area input:focus {border-color: #42b883;}
.input-area button {padding:12px 20px; background: #42b883; color:white;
border: none; border-radius: 6px; cursor: pointer; font-weight: bold; font-size: 15px;}

.checkbox { width: 18px; height: 18px; cursor: pointer;}
.completed {text-decoration: line-through; color: #9e9e9e;}
</style>
