<script setup>
import { reactive, ref } from "vue";

// ref
// Primitiv string, number, bool, dst.

const nama = ref("Anton 🙅");
const page = ref("page1");

// reactive
// non primitive array & Object
const biodata = reactive({
  umur: "20 y.o",
  hobi: "Volly",
});

const todo = ref(null);
const mode = ref("add");
const selected = ref(null);
const todos = reactive([
  {
    id: 1,
    title: "belajar vue",
    completed: false,
  },
  {
    id: 2,
    title: "coding react",
    completed: true,
  },
  {
    id: 3,
    title: "coding angular",
    completed: false,
  },
]);
function createTodo() {
  if (mode.value === "add") {
    if (validateTodo()) {
      todos.unshift({
        id: Math.random(),
        title: todo.value,
        completed: false,
      });
      todo.value = null;
    }
  } else {
    if (validateTodo()) {
      const index = todos.findIndex((e) => e.id === selected.value.id);
      todos[index].title = todo.value;
      todo.value = null;
      mode.value = "add";
    }
  }
}

function validateTodo() {
  return todo.value.trim();
}

function checkList(id) {
  if (todos[id].completed) {
    todos[id].completed = false;
  } else {
    todos[id].completed = true;
  }
}
function delTodo(idx) {
  todos.splice(idx, 1);
}

setTimeout(() => {
  // Ketika sudah 2 detik jalanin ini
  nama.value = "berubah 🦹‍♂️";
  biodata.hobi = "Menjadi Pahlawan";
}, 2000);

// const bil1 = ref(null);
// const bil2 = ref(null);
// const hasil = ref(null);

// function hitung() {
//   hasil.value = bil1.value + bil2.value;
// }
</script>
<template>
  <div class="container">
    <h1>{{ nama }}</h1>
    <p>Umur : {{ biodata.umur }}</p>
    <p>Hoby: {{ biodata.hobi }}</p>
  </div>
  <hr />
  <!-- <h1>All Todos</h1> -->

  <!-- const todo = ref(null) -->
  {{ todo }}
  <form @submit.prevent="createTodo">
    <input type="text" placeholder="todo...." v-model="todo" />
    <button type="submit">💾 {{ mode == "add" ? "simpan" : " edit" }}</button>
  </form>
  <br />
  <form>
    <input type="search" placeholder="🔍....." />
    <button type="button">🔍Search</button>
  </form>

  <div v-if="page === 'page1'" class="wrapper">
    <h2>All Todos</h2>
    <ul v-for="(item, index) in todos" :key="item.id" style="display: flex">
      <li @click="checkList(index)" :class="item.completed ? 'completed' : ''">
        {{ item.title }}
      </li>
      <button
        style="margin-right: 10px"
        @click="
          mode = 'edit';
          selected = item;
          todo = item.title;
        "
      >
        ✍️
      </button>
      <button @click="delTodo(index)">❌</button>
    </ul>
  </div>

  <div
    v-if="page === 'page2'"
    class="wrapper"
    style="background-color: greenyellow"
  >
    <h2>completed todos</h2>
  </div>

  <div v-if="page === 'page3'" class="wrapper">
    <h2>uncompleted todos</h2>
  </div>
  <div class="btn">
    <button @click="page = 'page1'" :class="page === 'page1' ? 'active' : ''">
      All Todos
    </button>
    <button @click="page = 'page2'" :class="page === 'page2' ? 'active' : ''">
      completed Todos
    </button>
    <button @click="page = 'page3'" :class="page === 'page3' ? 'active' : ''">
      uncompleted Todos
    </button>
  </div>
  <!-- <input type="number" @input="(event) => (bil1 = event.target.value)" /> +
  <input type="number" v-model="bil2" />
  <button @click="hitung">Hasil</button>
  <br />
  <p>Hasil : {{ hasil }}</p> -->
</template>
<style>
body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center;
  font-family: "Times New Roman", Times, serif;
  text-transform: capitalize;
}
.container {
  border: 1px solid;
  max-width: 400px;
  padding: 1 rem;
}
.active {
  background-color: aqua;
}
.completed {
  text-decoration: line-through;
  color: gray;
}
.input todo {
  display: flex;
}
.checkList {
  display: flex;
}
</style>
1
