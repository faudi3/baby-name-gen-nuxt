<script setup lang="ts">
import { Gender, Length, names, Popularity } from "@/data";
import { reactive } from "vue";
import { filter } from "rxjs";

interface OptionState {
  gender: Gender;
  popularity: Popularity;
  length: Length111235435;
}

const options = reactive<OptionState>({
  gender: Gender.GIRL,
  length: Length.LONG,
  popularity: Popularity.UNIQUE,
});

const removeName = (idx: number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(idx, 1);
  selectedNames.value = filteredNames;
};

const selectedNames = ref<string[]>([]);

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });
  selectedNames.value = filteredNames.map((name) => name.name);
};

const optionsArray = [
  {
    title: "1) Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.UNISEX, Gender.BOY],
  },
  {
    title: "2) Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3) Choose name's length",
    category: "length",
    buttons: [Length.SHORT, Length.ALL, Length.LONG],
  },
];
</script>

<template>
  <div class="container">
    <h1>Baby name generator</h1>
    <p>Choose your options and click the FInd names button below</p>
    <div class="options-container">
      <Option
        v-for="option in optionsArray"
        :key="option.title"
        :option="option"
        :options="options"
      />
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <CardName
        v-for="(name, idx) in selectedNames"
        :key="name"
        :name="name"
        @remove="() => removeName(idx)"
        :idx="idx"
      />
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

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
.cards-container {
  display: flex;
  margin-top: 3rem;
  flex-wrap: wrap;
}
</style>
