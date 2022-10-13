<script setup>
//metodo - methods
import { computed, ref } from "vue";
const counter = ref(0); //Counter se vuelve en un objeto reactivo
const ArrayNumbers = ref([]);

const increment = () => {
  counter.value++;
};
const decrement = () => {
  counter.value--;
};
const restart = () => {
  counter.value = 0;
};

const classCounter = computed(() => {
  if (counter.value == 0) {
    return "zero";
  }
  if (counter.value > 0) {
    return "positive";
  } else {
    return "negative";
  }
});

const add = () => {
  ArrayNumbers.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = ArrayNumbers.value.find((num) => num === counter.value);

  if (numSearch === 0) return true;
  return numSearch ? true : false;

  /*  return numSearch || numSearch === 0; */
});
</script>

<template>
  <div class="container text-center">
    <h1>VUE DINAMICO</h1>
    <h2 :class="classCounter">
      {{ counter }}
    </h2>
    <div class="btn-group">
      <button @click="decrement" class="btn btn-danger">Disminuir</button>
      <button @click="restart" class="btn btn-warning">Reniciar</button>
      <button @click="increment" class="btn btn-success">Aumentar</button>
      <button :disabled="bloquearBtnAdd" class="btn btn-primary" @click="add">
        Add
      </button>
    </div>
    <div>Numeros favoritos</div>
    <li v-for="numero in ArrayNumbers" :key="numero" class="list-group">
      <ul class="list-group-item">
        {{
          numero
        }}
      </ul>
    </li>
  </div>
</template>

<style>
h1 {
  color: red;
}
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: peru;
}
</style>
