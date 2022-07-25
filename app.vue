<script setup lang="ts">
import { IPVersion } from 'net';

enum TNamePopularity {
  TRENDY = 1,
  UNIQUE = 2
}
enum TNameGender {
  BOY = 1,
  GIRL = 2,
  UNISEX = 3
}
enum TNameLength {
  LONG = 1,
  SHORT = 2,
  ALL = 3,
}

interface IOptions {
  gender: TNameGender,
  popularity: TNamePopularity,
  length: TNameLength
}
type TProperties = keyof IOptions
const a: number = 2

console.log(a);

const options = reactive<IOptions>({
  gender: TNameGender.BOY,
  popularity: TNamePopularity.TRENDY,
  length: TNameLength.ALL
})

function onOptionClick (which: keyof IOptions, event: Event) {
  const option = event.target as HTMLButtonElement
  if (option.matches('.option[data-option]')) {
    const a = +option.dataset.option as TNameGender | TNameLength | TNamePopularity
    options[which] = a
  }
}


</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your option and click 'Find names' button below</p>
    <div class="options-container">
      <div class="option-container" @click="onOptionClick('gender', $event)">
        <h4>1) Choose a gender</h4>
        <button 
          :data-option="TNameGender.BOY" 
          :class="{'active': options.gender === TNameGender.BOY}" 
          class="option"
        >
          Boy
        </button>
        <button 
          :data-option="TNameGender.UNISEX" 
          :class="{'active': options.gender === TNameGender.UNISEX}" 
          class="option"
        >
          Unisex
        </button>
        <button 
          :data-option="TNameGender.GIRL" 
          :class="{'active': options.gender === TNameGender.GIRL}" 
          class="option" 
        >
          Girl
        </button>
      </div>
      <div class="option-container" @click="onOptionClick('popularity', $event)">
        <h4>1) Choose the name's popularity</h4>
        <button 
          :data-option="TNamePopularity.TRENDY" 
          :class="{'active': options.popularity === TNamePopularity.TRENDY}" 
          class="option"
        >
          Trendy
        </button>
        <button 
          :data-option="TNamePopularity.UNIQUE" 
          :class="{'active': options.popularity === TNamePopularity.UNIQUE}" 
          class="option"
          >
          Unique
        </button>
      </div>
      <div class="option-container" @click="onOptionClick('length', $event)">
        <h4>1) Choose the name's length</h4>
        <button
          :data-option="TNameLength.ALL" 
          :class="{'active': options.length === TNameLength.ALL}" 
          class="option"
        >
            All
        </button>
        <button 
          :data-option="TNameLength.LONG" 
          :class="{'active': options.length === TNameLength.LONG}" 
          class="option"
        >
          Long
        </button>
        <button 
          :data-option="TNameLength.SHORT" 
          :class="{'active': options.length === TNameLength.SHORT}" 
          class="option"
          >
            Short
          </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  margin: auto;
  text-align: center;
  max-width: 800px;
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(86, 86, 205);
}

h1 {
  font-size: 3rem;
}

.options-container {
background-color: antiquewhite;
padding: 0.4rem 1rem 1rem;
border-radius: 2rem;
width: 95%;
margin: 4rem auto 0;
position: relative;
}

.option {
background-color: white;
outline: .15rem solid rgb(249, 87, 89);
border: none;
padding: 0.75rem;
width: 12rem;
font-size: 1rem;
color: rgb(27, 60, 140);
font-weight: 200;
cursor: pointer;
transition: background-color 0.4s;
}
.option:hover {
background-color: rgb(249, 87, 89);
}
.option.active {
background-color: rgb(249, 87, 89);
}
.options-container .option:first-of-type {
border-radius: 1rem 0 0 1rem;
}
.options-container .option:last-of-type {
border-radius: 0 1rem 1rem 0;
}
</style>