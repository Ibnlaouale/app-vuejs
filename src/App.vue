<template>
  <h1>App vue js</h1>
  <p id="pName">Hello..!! my name is : {{ firstName }}</p>
  <div class="btn">
    <button @click="increment">incrementer</button>
    <button @click="decrement">Decrementer</button>
  </div>
  <p class="p">{{ count }}</p>
</template>

<script setup>
import { ref } from 'vue';
const firstName = 'Dini'

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
#pName{
  color: blue;
}
.btn {
  width: 40rem;
  display: flex;
  justify-content: space-evenly;
}
.btn button{
  padding: 5px;
  border-radius: 10px;
  cursor: pointer;
  color: blue;
  border: .5px solid;
  font-size: 16px;
  background-color: white;
}

.p {
  color: green;
  width: 40rem;
  text-align: center;
  font-size: 32px;
  font-weight: bold;
}
</style>