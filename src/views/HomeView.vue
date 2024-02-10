
<template>
<main>
<div class="main_div">
  <h1>Todo Lists</h1>
  <el-date-picker
        v-model="data_val"
        type="date"
        placeholder="Pick a day"
        value-format="YYYY/MM/DD"
      />
      <button @click="add_data()" class="w-[100px] p-[5px] bg-[#000] text-white">data</button>
  <input type="text" placeholder="new todo" v-model="todo_input">
  <button class="button" @click="addTodo">add</button>
  <ul class="ul">
    <li v-for="(todo,i) in todos" :key="todo.id" style="display: flex; gap: 10px; align-items: center;">
      <p class="p_text" :class="{
        completed_todo: todo.is_completed,
      }">{{ i + 1 }}.   {{ todo.title }}.{{ todo.date }}</p>
      <button class="end_btn" @click="completed_line(todo.id)">end</button>
      <button class="delete_btn" @click="deleteTask(todo.id)">delete</button>
    </li>
  </ul>
</div>
</main>
<div v-for="user in users" :key="user.id">
    <RouterLink :to="'/user/' + user.id">{{ user.name }}</RouterLink>
  </div>
</template>

<script setup>
const data_val = ref(null)


const add_data = () => {
  console.log(data_val.value);
}
import { ref } from "vue"
const todo_input = ref("")
const todos = ref([
  {
    id:1, 
    title:"task1",
    is_completed: true,
  }
])
const addTodo = () => {
  const new_todo = {
    id:new Date().getTime(),
    title:todo_input.value,
    is_completed: false,
    date:data_val.value
  }
  todos.value.push(new_todo)
}
const completed_line = (id,i) => {
  const index = todos.value.findIndex((todo) => todo.id == id);
  todos.value[index].is_completed = !todos.value[index].is_completed;
}
const deleteTask = (id) => {
  const filtered_task = todos.value.filter((todo) => todo.id != id)
  todos.value = filtered_task

}
const users = [
  {
    id:1,
    name:"user1"
  },
  {
    id:2,
    name:"user2"
  },
]
</script>
<style>
.completed_todo {
  text-decoration: line-through;
}
main {
  display: flex;
  justify-content: center;
  
}
input {
  padding: 15px;
  width: 300px;
  border: none;
  border-radius: 20px;
  margin-top: 20px;
}
.button {
  margin-left: 20px;
  padding: 10px;
  border: none;
  width: 200px;
  background-color: blueviolet;
  color: white;
  border-radius: 7px;
}
.p_text {
  font-size: 24px;
}
.end_btn {
  padding: 7px;
  width: 100px;
  background-color: blue;
  border: none;
  border-radius: 7px;
  color: white;
}
.delete_btn {
  padding: 7px;
  width: 100px;
  background-color: darkcyan;
  border: none;
  border-radius: 7px;
  color: white;
}
.main_div {
  padding: 20px;
  border-radius: 30px;
  background-color: antiquewhite

}
ul {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
li {
  padding-left: 20px;
  padding-right: 20px;
  border-radius: 20px;
  background-color: azure;
}
input:focus {
  outline: none;
}
  

</style>