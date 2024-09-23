<template>
  <h1 :style="{ color: count > 5 ? 'red' : 'green' }">App vue js <span v-html="learn"></span></h1>
  <p id="pName">Hello..!! my name is : {{ firstName }}</p>
  <div class="btn">
    <button @click="increment">incrementer</button>
    <button @click="decrement">Decrementer</button>
    <button @click="reorganiser">Reorganiser</button>
  </div>
  <p :id="`p-${count}`" class="p">{{ count }}</p>
  <div v-if="count > 5">Attention vous avez cliquez plus de 5 fois...!!!</div>
  <hr>
  <form @submit.prevent="addMovie">
    <h3>Ajouter un nouveau film</h3>
    <label for="">Titre du film :</label>
    <input type="text" placeholder="nouveau film" v-model="movieName">
    <button class="btnAdd" type="submit">Ajouter</button>
  </form>
  <h2>liste des films</h2>
  <ul>
    <li :style="{ color: 'blue' }" v-for="movie in movies" :key="movie">{{ movie.toUpperCase() }} <button
        @click="deleteMovie(movie)">Delete</button></li>
  </ul>
  <hr>
  <div>
    <h3>Affiche les information d'un objet:</h3>
    <ul>
      <li>Nom: {{ personne.firstName }}</li>
      <li>Prnom: {{ personne.lastName }}</li>
      <li>Age: {{ personne.age }}</li>
      <button @click="changeAge">Modifier age</button>
    </ul>
  </div>

  <!-- ======================TP-TodoList=============== -->
  <hr>
  <div :style="{ background: 'midnightblue', padding: '10px', textAlign: 'center', color:'yellow' }">
    <h2>TP-TodoList</h2>
    <form action="" @submit.prevent="AddTask">
      <label for="">
        <input type="text" placeholder="nouvelle tâche" v-model="newTask">
        <button :disabled="newTask.length === 0" type="submit">Ajouter</button>
      </label>
    </form>
    <p v-if="taches.length === 0">Aucune tâches</p>
    <ul>
      <li :class="{completed: tache.complete}"  v-for="tache in sortedtodo()" :key="tache.date"> {{ tache.titre }} <input type="checkbox" v-model="tache.complete"></li>
    </ul>
    <label> 
      <input type="checkbox" v-model="hideCompleted">
      Masquer les tâches effectuées
    </label>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const firstName = 'Dini'
const learn = "<i>by practice</i>"
const count = ref(0)
console.log('count :', count);

const increment = () => {
  count.value++
}

const movies = ref([
  'zombie',
  'anime',
  'box',
  'action',
  'foret'
])

const deleteMovie = (movie) => {
  movies.value = movies.value.filter(film => film != movie);
}

const reorganiser = () => {
  movies.value = movies.value.sort((a, b) => a > b ? 1 : -1)
}

const decrement = () => {
  if (count.value <= 0) {
    count.value = 0;
    return;
  }
  count.value--
}

// Ajout de film

const movieName = ref('');

const addMovie = () => {
  if (movieName.value.trim() === '') {
    alert('veuillez renseigner le champ...!!!')
    movieName.value = '';
    return
  }

  const titleMovie = movieName.value;
  movies.value = [...movies.value, titleMovie];
  movieName.value = '';
  alert('film ajouter avec succèes')

}

// les objets
const personne = ref({
  firstName: 'Jonh',
  lastName: 'Doe',
  age: 20
})

const changeAge = () => {
  personne.value.age = Math.round(Math.random() * 100)
}

//=================== TP-TodoList===============

const taches = ref([
  {
    titre: 'todo test completed',
    complete: true,
    date: 1
  },
  {
    titre: 'todo test incompleted',
    complete: false,
    date: 2
  }
])
const newTask = ref('');

const AddTask = () => {
    if (newTask.value.trim() === '') {
      alert('veuillez renseigner le champ...!!!');
      newTask.value = '';
      return; 
    }
  const task = {
    titre: newTask.value,
    complete: false,
    date: Date.now()
  }

  taches.value.push(task);
  newTask.value = '';
}

const hideCompleted = ref(false)
const sortedtodo = () => {
  const sortedtodo = taches.value.toSorted((a, b) => a.complete > b.complete ? 1 : -1);
  if (hideCompleted.value === true) {
    return taches.value.filter(t => t.complete === false)
}
 return sortedtodo;
}


</script>



<style>
#pName {
  color: blue;
}
.completed{
  opacity: 5;
  text-decoration: line-through;
}
.btn {
  width: 40rem;
  display: flex;
  justify-content: space-evenly;
}

.btnAdd {
  padding: 5px;
  border-radius: 5px;
  border: none;
  margin-left: 5px;
  background-color: black;
  color: white;
  cursor: pointer;
}

.btnAdd:hover {
  background-color: white;
  color: black;
  border: 1px solid;
}


.btn button {
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