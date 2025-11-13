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

  const classCounter = computed(() => {
    if (counter.value === 0) {
      return 'cero';
    }
    if (counter.value > 0) {
      return 'positivo';
    }
    if (counter.value < 0) {
      return 'negativo';
    }
  });

  const listaFavoritos = ref([]);

  const añadirAFavoritos = () => {
    listaFavoritos.value.push(counter.value);
  };

  const bloquearAñadirAFavoritos = computed(() => {
    // let bloquear = false;
    const numeroAComprobar = listaFavoritos.value.find(
      (numero) => numero === counter.value
    );
    // if (numeroAComprobar || numeroAComprobar===0) bloquear = true;
    // return numeroAComprobar || numeroAComprobar == 0 ? true : false;
    return numeroAComprobar || numeroAComprobar == 0;
  });
</script>

<template>
  <!-- <h1>Hola {{ name }}!</h1> -->

  <!-- <h2 :class="counter >0 ? 'positivo' : 'negativo'">{{ counter }}</h2> -->

  <div class="container text-center mt-3">
    <h2 :class="classCounter">{{ counter }}</h2>

    <!-- <button @click="increment()">Aumentar</button> -->
    <div class="btn-group">
      <button @click="counter++" class="btn btn-success">
        Aumentar con Integración
      </button>
      <button @click="counter--" class="btn btn-danger">
        Disminuir con Integración
      </button>
      <button @click="counter = 0" class="btn btn-secondary">
        Poner a cero
      </button>
      <button
        @click="añadirAFavoritos"
        :disabled="bloquearAñadirAFavoritos"
        class="btn btn-primary"
      >
        Añadir a favoritos
      </button>
    </div>
    <br /><br />
    {{ listaFavoritos }}

    <ul class="list-group mt-4">
      <li
        class="list-group-item"
        v-for="(numero, index) in listaFavoritos"
        :key="index"
      >
        {{ numero }}
      </li>
    </ul>
  </div>
</template>

<style></style>
