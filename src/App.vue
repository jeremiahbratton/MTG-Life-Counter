<script setup>
import { ref } from 'vue';
import { identities } from './assets/modules/mana';

const options = ref({
  colors: [],
  identity: 'white',
  startingLife: 20,
  currentLife: 20,
  mode: 'standard'
});

const optionsVisible = ref(false);

function changeLife(direction) {
  if (direction) {
    options.value.currentLife++;
  } else {
    options.value.currentLife--;
  }
}

function resetLife(amount = null) {
  if (amount) {
    options.value.startingLife = amount;
  }

  options.value.currentLife = options.value.startingLife;
}

function toggleOptionsPanel() {
  console.log(optionsVisible.value);
  optionsVisible.value = optionsVisible.value ? false : true;
}

function changeIdentity(color) {
  options.value.identity = color;
}
</script>

<template>
  <main :class="`counterBody identity-${options.identity}`">
    <img :src="`/${options.identity}.svg`" class="identity-icon" width="160" height="160" />
    <div class="lifeCounter">
      <button @click.prevent="changeLife(false)" class="roundButton">-</button>
      <span class="life-total">{{ options.currentLife }}</span>
      <button @click.prevent="changeLife(true)" class="roundButton">+</button>
    </div>

    <button @click="toggleOptionsPanel" class="optionsButton">...</button>
    <div v-if="optionsVisible" class="options-panel">
      <section>
        <h2>Starting Life</h2>
        <div class="starting-life-buttons">
          <button @click="resetLife(20)" class="starting-life-button">20</button>
          <button @click="resetLife(30)" class="starting-life-button">30</button>
          <button @click="resetLife(40)" class="starting-life-button">40</button>
        </div>
      </section>

      <section>
        <h2>Identity</h2>
        <div class="options-identity-buttons">
          <button @click="changeIdentity('white')" class="color-button"><img src="/white.svg" width="60"
              height="60" /></button>
          <button @click="changeIdentity('blue')" class="color-button"><img src="/blue.svg" width="60"
              height="60" /></button>
          <button @click="changeIdentity('black')" class="color-button"><img src="/black.svg" width="60"
              height="60" /></button>
          <button @click="changeIdentity('red')" class="color-button"><img src="/red.svg" width="60"
              height="60" /></button>
          <button @click="changeIdentity('green')" class="color-button"><img src="/green.svg" width="60"
              height="60" /></button>
        </div>
      </section>
    </div>
  </main>
</template>
