<script setup>
  const name = 'Vue dinámico';
  const styleColor = 'color: blue';
  const arrayColores = ['blue', 'red', 'peru'];
  const color = 0;
  const activo = true;
  const arrayFrutas = ['🍎', '🍌', '🍉', '🍓', '🍒'];
  const arrayFrutasLdeO = [
    {
      name: 'Manzana',
      price: '$1.00',
      description: 'Una manzana',
      stock: 0,
    },
    {
      name: 'Pera',
      price: '$2.00',
      description: 'Una pera',
      stock: 10,
    },
    {
      name: 'Naranja',
      price: '$3.00',
      description: 'Una naranja',
      stock: 20,
    },
  ];

  const objetoFruta = {
    name: 'Manzana',
    price: '$1.00',
    description: 'Una manzana',
    id: 1,
  };
</script>

<!-- Un Template sirve para renderizar -->
<template>
  <ul>
    <template v-for="item in arrayFrutasLdeO" :key="item.name">
      <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }}</li>
    </template>
  </ul>

  <br />
  <br />
  <br />

  {{ objetoFruta }}

  <ul>
    <li v-for="(value, propiedad, index) in objetoFruta" :key="value">
      {{ index }} - {{ propiedad }}: {{ value }}
    </li>
  </ul>

  <br /><br />

  <ul>
    <li v-for="(objeto, index) in arrayFrutasLdeO" :key="objeto.name">
      <div>
        <p>Nombre: {{ objeto.name }}</p>
        <p>Precio: {{ objeto.price }}</p>
        <p>Descripción: {{ objeto.description }}</p>
      </div>
    </li>
  </ul>
  <br />
  <ul>
    <li v-for="(fruta, index) in arrayFrutas" :key="index">
      {{ index }} {{ fruta }}
    </li>
  </ul>
  <br />

  <h1>Hola {{ name.toUpperCase() }}</h1>
  <h2>{{ arrayColores }}</h2>
  <!-- <h2 v-bind:style="styleColor">Soy azul</h2> -->
  <h2 :style="styleColor">Soy azul</h2>
  <!-- <h2 :style="`color:${arrayColores[color]}`">`Soy el color ${{ arrayColores[color] }}`</h2> -->
  <h2 :style="{ color: arrayColores[color] }">
    Soy el color {{ arrayColores[color] }}
  </h2>
  <h2>
    {{ activo ? 'Estoy activo' : 'Estoy inactivo' }}
  </h2>

  <p v-if="activo">Estoy activo con v-if</p>
  <p v-else-if="!activo">Estoy inactivo con v-if</p>
  <p v-else>Estoy indeciso con v-if</p>

  <h2 v-show="activo">Estoy activo con v-show</h2>
</template>

<style>
  h1 {
    color: red;
  }
</style>
