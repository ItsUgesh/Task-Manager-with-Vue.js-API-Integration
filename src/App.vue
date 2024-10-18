<script setup>
import { ref,onMounted } from "vue";

const name = ref("ugesh simkhada");
const status = ref("active");
const cars = ref(["honda", "tesla", "lamborgini", "toyota", "supra"]);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'inactive';
  } else {
    status.value = 'active';
  }
}

const addTask = () => {
  if (newTask.value.trim() !== '') {
    cars.value.push(newTask.value);
    newTask.value = '';
  }
}

const deleteTask = (index) => {
  cars.value.splice(index, 1);
}

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    cars.value = data.slice(0,7).map((car)=>car.title)
  } catch (error) {
    console.log("error fetching data");
  }
})


</script>

<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">Use is active</p>
  <p v-else-if="status === 'pending'">Use is pending</p>
  <p v-else>Use is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">New Task: </label>
    <input type="text" name="newTask" id="newTask" v-model="newTask">
    <button type="submit">ADD</button>
  </form>
  <br>
  <h3>List of Cars</h3>
  <ul>
    <li v-for="(car, index) in cars" :key="car">
      <span>
         {{ car }}
      </span>
      <button v-on:click="deleteTask(index)">  x</button>
    </li>
  </ul>
  <a href="https://ugeshsimkhada.com.np">it'a a link</a>
  <br>
  <Button @click="toggleStatus">change status</Button>
</template>
