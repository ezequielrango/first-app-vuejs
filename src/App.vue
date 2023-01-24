<!-- Single File Component 

Podemos tener estructura, lógica y estilos. -->

<script setup>
import {ref, computed} from 'vue';

  const name = 'vue dinámico';
  const styleColor = 'color:blue';
  const arrayColores = ['blue','red', 'green'];
  const activo = true;
  const arrayFrutas = [
    {
      name: 'Manzana',
      price: '$1.00',
      description: 'Una manzana',
      stock: 0
    },
    {
      name: 'Pera',
      price: '$1.00',
      description: 'Una Pera',
      stock: 15
    },
    {
      name: 'Banana',
      price: '$1.00',
      description: 'Una Banana',
      stock: 25
    }
  ];

  const frutaObjeto =     {
      name: 'Manzana',
      price: '$1.00',
      description: 'Una manzana'
    }

    //metodo - methods

const handleClick = (msg) => {
  console.log(msg);
}
const arrayFavoritos = ref([])
const counter = ref(0); // con ref indicamos que es una variable reactiva

const increment = () => {
  counter.value ++ // .value porque cuando se convierte en una variable reactiva vue lo transforma en un objeto
}
const decrement = () => {
  counter.value --
}
const reset = () => {
  counter.value = 0;
}

const add = () => {
  arrayFavoritos.value.push(counter.value)
}
const bloquearBtnAdd = computed(() => {
  const numSearch = arrayFavoritos.value.find(num => num === counter.value);
  if(numSearch === 0) return true;
  return numSearch ? true : false;
})
const classCounter = computed(() => {
  if(counter.value === 0){
    return 'zero'
  }
  if(counter.value > 0) {
    return 'positive'
  }
  if (counter.value < 0) {
    return 'negative'
  }
})
</script>

<template>

  <!-- se pueden usar expresiones de js -->
  <h1>Hola {{ name.toUpperCase() }}</h1> 
  <!-- //v-bind o : para insertar variables en atributos, permite la comunicacion entre script y el template -->
  <!-- <h2>{{ arrayColores }}</h2>
  <h2 v-bind:style="`color: ${arrayColores[0]}`"> Texto azul</h2>  -->
  <h2>
    <!-- {{ activo ? 'estoy activo' : 'estoy inactivo' }} -->
  </h2>
  <!-- <h2 v-if="activo">Estoy activo</h2> -->
   <!-- else debe ir seguido de if -->
  <!-- <h2 v-else="!activo">Estoy inactivo</h2> -->
  <!-- Se mantiene en la estructura HTML sin importar el valor booleano, pero cambia el display none -->
  <!-- <h2 v-show="activo" > Estoy activo v-show</h2>  -->
  <!-- <ul> -->
    <!-- v-if dentro del v-for no puede ir directo porque for tiene mas peso -->
    <!-- <template  v-for="fruta in arrayFrutas" :key="fruta.name">
      <li v-if="fruta.stock > 0">
          {{ fruta.name }} - {{ fruta.price }} - {{ fruta.description }} {{ fruta.stock }}
      </li>
    </template>
  </ul> -->

  <!-- <ul> -->
    <!-- recorrer un objeto -->
    <!-- <li  v-for="(value, propiedad, index) in frutaObjeto" :key="value">
    {{ index }} - {{ propiedad }} : {{ value }}
    </li>
  </ul> -->

  <!-- Evento Onclick y modificadores -->

  <!-- <button v-on:click.right="handleClick('mensaje right')">Activame right</button>
  <button @click.left="handleClick('mensaje left')">Activame left</button>
  <button @click.middle="handleClick('mensaje middle')">Activame middle</button> -->

  <div class="container text-center mt-3">
    <div class="btn-group">
      <button @click="increment()" class="btn btn-success">AUMENTAR</button>
      <button @click="decrement()" class="btn btn-danger">DISMINUIR</button>
      <button @click="reset()" class="btn btn-secondary">REINICIAR</button>
      <button @click="add" :disabled="bloquearBtnAdd" class="btn btn-primary">Add</button>
    </div>
    <h2 :class="classCounter">{{ counter }}</h2>
  
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="(num, index) in arrayFavoritos" :key="index"
      >
      {{ num }}
    </li>
    </ul>

  </div>
</template>

<style>
  h1 {
    color: red
  }
  .positive {
    color : green
  }
  .negative{
    color: red
  }
  .zero{
    color: peru
  }
</style>