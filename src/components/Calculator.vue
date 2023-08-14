
<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div class="btn" @click="clear">C</div>
    <div class="btn" @click="sign">+/-</div>
    <div class="btn" @click="percent">%</div>
    <div @click="append('/')" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="append('*')" class="btn operator">*</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="append('-')" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="append('+')" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="calc" class="btn operator">=</div>
  </div>
</template>

<script setup>
import {ref} from 'vue'

const current = ref('0');
const clear = () => {
  current.value = 0;
}

const sign = () => {
  current.value = current.value.charAt(0) === '-' ? current.value.slice(1) : `-${current.value}` 
}

const percent = () => {
  current.value = `${parseFloat(current.value * 0.01)}`;
}

const append = (number) => {
  if(current.value === 0){
    current.value = `${number}`;
  } else {
    current.value = `${current.value}${number}`;
  }
}

const dot = () => {
  if(current.value.indexOf('.') === -1){
    append('.')
  }
}

const calc = () => {
  current.value = eval(current.value)
}

</script>

  

<style scoped>
  .calculator {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    grid-auto-rows: minmax(50px, auto);
    width: 400px;
    margin: 0 auto;
    height: auto;
    background-color: gray;
    font-size: 40px;
  }
  .display {
    grid-column: 1 / 5;
    background-color: #333;
    color: white;
  }
  .zero {
    grid-column: 1 / 3;
  }
  .calculator > div {
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .btn {
    background-color: #F2F2F2;
    border: 1px solid #999;
  }
  .operator {
    background-color: orange;
    color: white;
  }

</style>