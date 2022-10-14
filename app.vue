<script setup lang="ts">
enum Gender {
  GIRL = "Girl",
  BOY = "Boy",
  UNISEX = "Unisex",
}

enum Popularity {
  TRENDY = "Trendy",
  UNIQUE = "Unique",
}

enum Length {
  SHORT = "Short",
  LONG = "Long",
  ALL = "All",
}

interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length;
}

import { reactive } from "vue";

const options = reactive<OptionState>({
  gender: Gender.GIRL,
  length: Length.LONG,
  popularity: Popularity.UNIQUE,
});
</script>

<template>
  <div class="container">
    <h1>Baby name generator</h1>
    <p>Choose your options and click the FInd names button below</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1) choose a gender</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="options.gender === Gender.BOY && 'option-active'"
            @click="options.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="option"
            :class="options.gender === 'Girl' && 'option-active'"
            @click="options.gender = Gender.GIRL"
          >
            Girl
          </button>
          <button
            class="option option-right"
            :class="options.gender === 'Unisex' && 'option-active'"
            @click="options.gender = Gender.UNISEX"
          >
            Unisex
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) choose the names popularity</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="options.popularity === 'Trendy' && 'option-active'"
            @click="options.popularity = Popularity.TRENDY"
          >
            trendy
          </button>
          <button
            class="option option-right"
            :class="options.popularity === 'Unique' && 'option-active'"
            @click="options.popularity = Popularity.UNIQUE"
          >
            unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) choose a the length of the name</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="options.length === 'Long' && 'option-active'"
            @click="options.length = Length.LONG"
          >
            long
          </button>
          <button
            class="option"
            :class="options.length === 'All' && 'option-active'"
            @click="options.length = Length.ALL"
          >
            all
          </button>
          <button
            class="option option-right"
            :class="options.length === 'Short' && 'option-active'"
            @click="options.length = Length.SHORT"
          >
            short
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.container {
  font-family: "Helvetica", sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
}
.container h1 {
  font-size: 3rem;
  text-align: center;
}
p {
  text-align: center;
}
h4 {
  text-align: center;
}
.options-container {
  background-color: rgb(255, 238, 236);
  padding: 1rem;
  border-radius: 2rem;
  width: 95%;
  margin: 2rem auto;
  text-align: center;
  position: relative;
}
.option-container {
  margin-bottom: 2rem;
}
.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;

  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 600;
}
.option-left {
  border-radius: 1rem 0 0 1rem;
}
.option-right {
  border-radius: 0 1rem 1rem 0;
}
.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}
</style>
