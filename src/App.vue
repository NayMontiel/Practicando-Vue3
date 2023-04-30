<script setup>
import { computed, ref } from 'vue';

const name = "Vue 3";
const styleColor = "color: lightgreen";
const arrayColor = ["lightblue", "red", "yellow"];
const active = true;
const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒", "🍐", "🍊"];
const arrayDeFrutas = [
  {
    name: "Manzana 🍎",
    price: "$1.00",
    description: "Una manzana",
  },
  {
    name: "Pera 🍐",
    price: "$2.00",
    description: "Una pera",
  },
  {
    name: "Naranja 🍊",
    price: "$3.00",
    description: "Una naranja",
  },
];
const objetoFrutas = {
  name: "Banana 🍌",
  price: "$1.00",
  description: "Una Banana",
};

const frutas = [
  {
    name: "Manzana 🍎",
    price: "$1.00",
    description: "Una manzana",
    stock: 0,
  },
  {
    name: "Pera 🍐",
    price: "$2.00",
    description: "Una pera",
    stock: 10,
  },
  {
    name: "Naranja 🍊",
    price: "$3.00",
    description: "Una naranja",
    stock: 20,
  },
  {
    name: "Banana 🍌",
    price: "$1.00",
    description: "Una Banana",
    stock: 15,
  },
];
//methods - metodo

const handleClick = (msj) => {
  console.log(msj)
}
//contador
let counter = ref(0);
const favoritos = ref([]);

const increment = () => {
  counter.value++;
  // console.log(counter);
}
const decrement = () => {
  counter.value--;
  // console.log(counter);
}
const reset = () => {
  counter.value =0
  // console.log(counter)
}

const add = () => {
 favoritos.value.push(counter.value)
  // console.log(counter)
}

const addDisabled = computed(() => {
  const numSearch = favoritos.value.find( (num) => num === counter.value);
  console.log(numSearch) 
  return numSearch || numSearch === 0;
})

const classCounter = computed(() => {
  if (counter.value === 0) {
    return 'cero'
  }
  if (counter.value > 0) {
    return 'positivo'
  } if (counter.value < 0) {
    return 'negativo'
  }
 
})

</script>

<template>
  <div class="container">
    <h1>Mi Primer App Con {{ name.toUpperCase() }}</h1>
  <h2 v-bind:style="styleColor">Soy un Parrafo</h2>
  <h3 :style="`color: ${arrayColor[2]}`">Probando Array</h3>
  <h4>{{ active ? "Estoy Activo" : "Estoy Inactivo" }}</h4>
  <h4 :style="`color: ${arrayColor[1]}`" v-if="active === true">
    Estoy Activo Usando v-if
  </h4>
  <h4 :style="`color: ${arrayColor[0]}`" v-else-if="active === false">
    Estoy Inactivo Usando v-else-if
  </h4>
  <h3 :style="styleColor" v-show="active">Actiivo Usando v-show</h3>
  <h2 class="text-info mb-3 mt-3">Recirriendo un array de frutas</h2>
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index">
      {{ index }} - {{ fruta }}
    </li>
  </ul>
  <h2 class="text-info mb-3 mt-3">Ejemplo Practico del V-for</h2>
  <ol>
    <li v-for="item in arrayDeFrutas" :key="name">
      {{ item.name }} - {{ item.price }} - {{ item.description }}
    </li>
  </ol>
  <h2 class="text-info mb-3 mt-3">Ejemplo recorriendo un objeto de fruta</h2>
  <ul>
    <li v-for="(value, propiedad, index) in objetoFrutas" :key="value">
      {{ index }} - {{ propiedad }} : {{ value }}
    </li>
  </ul>

  <h2 class="text-info mb-3 mt-3">Ejemplo usando v-for v-if</h2>
  <ol>
    <li v-for="item of frutas" :key="item">
      {{ item.name }} - {{ item.price }} - {{ item.stock }}
    </li>
  </ol>
  <h2 class="text-info mb-3 mt-3">Ejemplo usando ahora si v-if con v-for</h2>
  <ul>
    <template  v-for="item of frutas" :key="item">
    <li v-if="item.stock > 0">      
        {{ item.name }} - {{ item.price }}      
    </li>
    </template>
  </ul>
  <h2 class="text-info mb-3 mt-3">Eventos</h2>
  <button v-on:click.right.prevent="handleClick('click #1')" class="btn btn-outline-primary mx-2"> Haz Click Btn Right </button>
  <button @click.left="handleClick('click #2')" class="btn btn-outline-danger mx-2"> Haz Click  Btn Left </button>
  <button @click.middle="handleClick('click #3')" class="btn btn-outline-warning mx-2"> Haz Click Btn Middle </button>

  <h2 class="text-info mb-3 mt-3">Contador</h2>
  <h3 :class="classCounter ">{{ counter }}</h3>
  <button v-on:click="increment('incrementar')" class="btn btn-success mx-2"> INCREMENT </button>
  <button @click="decrement('decrementar')" class="btn btn-danger mx-2"> DECREMENT </button>
  <button @click="reset('reset')" class="btn btn-outline-primary mx-2"> RESET </button>
  <button @click="add" class="btn btn-warning mx-2" :disabled="addDisabled">AGREGAR</button>
  <ul class="mt-3">
    <li v-for="(num, index) in favoritos" :key="index" >
      {{ num }}
    </li>
  </ul>
  </div>
</template>

<style>
h1 {
  color: rgb(237, 95, 119);
}
.positivo{
  color: greenyellow;
}
.negativo {
  color: red;
}
.cero {
  color: palevioletred;
}
</style>
