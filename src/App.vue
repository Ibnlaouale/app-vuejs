<template>
  <h1>hello {{ firstName }}</h1>
  <p>test vue js</p>
  <div class="btn">
    <button @click="increment">incrementer</button>
    <button @click="decrement">Decrementer</button>
  </div>
  <p class="p">{{ count }}</p>
</template>

<script setup>
import { ref } from 'vue';
const firstName = 'Jonh Doe'

const count = ref(0)
console.log('count :', count);

const increment = () => {
  count.value++
}

const decrement = () => {
  count.value--
}
</script>

<style>
.btn {
  width: 40rem;
  display: flex;
  justify-content: space-evenly;
}

.p {
  width: 40rem;
  text-align: center;
  font-size: 32px;
  font-weight: bold;
}
</style>