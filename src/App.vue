<template>
  <div class="background">
    <img src="https://images.pexels.com/photos/1037992/pexels-photo-1037992.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1" />
  </div>
  <div class="content">
    <h1 :style="{ color: titleColor, fontWeight: titleWeight }">{{ title }}</h1>
    <div class="container">
      <form @submit.prevent="submitForm">
        <input type="number" v-model="inputNumber" class="input-number" placeholder="Masukan Nilai"/>
        <div class="button-container">
          <button type="button" @click="multiplyByTwo" class="btn">Plus</button>
          <button type="button" @click="divideByTwo" class="btn">Minus</button>
        </div>
      </form>
    </div>
    <p v-if="showResult" class="result">Nilai {{ inputNumber }} DI {{ action }} maka menjadi {{ result }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const title = ref('Plus Minus');
const titleColor = ref('white');
const titleWeight = ref('bold');
const inputNumber = ref('');
const result = ref('');
const action = ref('');
const showResult = ref(false);

function multiplyByTwo() {
  result.value = parseInt(inputNumber.value) * 2;
  action.value = 'Plus 2';
  showResult.value = true;
}

function divideByTwo() {
  result.value = parseInt(inputNumber.value) / 2;
  action.value = 'Minus 2';
  showResult.value = true;
}

function submitForm() {
  if (inputNumber.value >= 0) {
    multiplyByTwo();
  } else {
    divideByTwo();
  }
}
</script>

<style scoped>
.container {
  text-align: center;
}

.content {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 20px; 
  border: 1px solid #ccc;
  backdrop-filter: blur(5px);
  filter: drop-shadow(0 0 10px black);
}

.input-number {
  padding: 5px;
  margin-right: 10px;
  border: none; 
}

.button-container {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}

.btn {
  padding: 8px 20px;
  cursor: pointer;
  margin: 0 5px;
  border: 1px solid #ccc;
}

.result {
  margin-top: 20px;
  max-width: 100%;
  color: white;
  text-shadow: 0 0 10px black;
}

.background img {
  position: fixed;
  top: 0;
  left: 0;
  min-height: 90%;
  min-width: 1500px;
  width: 100%;
  height: 100%;
  overflow: hidden;
  z-index: -2;
  object-fit: cover;
  -webkit-background-size: cover;
  -moz-background-size: cover;
  -o-background-size: cover;
  background-size: cover;
  filter: brightness(0.8);
}
</style>
