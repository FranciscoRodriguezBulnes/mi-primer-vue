<script setup>
  import { ref, computed } from 'vue';

  const name = 'Vue 3';

  // método handleClick
  const handleClick = (message) => {
    console.log(message);
    alert(message);
  };

  const counter = ref(0);

  const increment = () => {
    console.log('first');
    counter.value++;
  };

  const classCounter = computed( () =>{
    if(counter.value === 0) {
      return 'cero'
    }
    if(counter.value >0) {
      return 'positivo'
    }
    if(counter.value < 0) {
      return 'negativo'
    }
  })
</script>

<template>
  <h1>Hola {{ name }}!</h1>

  <!-- <h2 :class="counter >0 ? 'positivo' : 'negativo'">{{ counter }}</h2> -->
  <h2 :class="classCounter">{{ counter }}</h2>

  <button @click="increment()">Aumentar</button>
  <button @click="counter++">Aumentar con Integración</button>
  <button @click="counter--">Disminuir con Integración</button>
  <button @click="counter = 0">Poner a cero</button>

  <br /><br /><br /><br /><br />

  <!-- Botón derecho: usar contextmenu -->
  <button @contextmenu.prevent="handleClick('Click Botón Derecho')">
    Click Botón Derecho
  </button>

  <!-- Botón izquierdo -->
  <button @click="handleClick('Click Botón Izquierdo')">
    Click Botón Izquierdo
  </button>

  <!-- Botón rueda/medio -->
  <button @mousedown.middle.prevent="handleClick('Click Rueda')">
    Click Rueda
  </button>
</template>


<style>
  h1 {
    color: red;
  }

  .positivo{
    color:green
  }

  .negativo {
    color:red
  }

  .cero {
    color:peru
  }
</style>