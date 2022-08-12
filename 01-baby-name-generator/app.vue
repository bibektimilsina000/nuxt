<template>
  <div class="container">
    <h1>Baby name generator</h1>
    <p>Choose your options and click the find names to get name</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="option.gender === Gender.BOY && 'option-active'"
            @click="option.gender = Gender.BOY"
          >
            Boy
          </button>
          <button
            class="option"
            :class="option.gender === Gender.UNISEX && 'option-active'"
            @click="option.gender = Gender.UNISEX"
          >
            Unisex
          </button>
          <button
            class="option option-right"
            :class="option.gender === Gender.GIRL && 'option-active'"
            @click="option.gender = Gender.GIRL"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose the name popularity</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="option.popularity === Popularity.TRENDY && 'option-active'"
            @click="option.popularity = Popularity.TRENDY"
          >
            TRENDY
          </button>
          <button
            class="option option-right"
            :class="option.popularity === Popularity.UNIQUE && 'option-active'"
            @click="option.popularity = Popularity.UNIQUE"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose The name length</h4>
        <div class="option-buttons">
          <button
            class="option option-left"
            :class="option.Length === Length.LONG && 'option-active'"
            @click="option.Length = Length.LONG"
          >
            Long
          </button>
          <button
            class="option"
            :class="option.Length === Length.ALL && 'option-active'"
            @click="option.Length = Length.ALL"
          >
            All
          </button>
          <button
            class="option option-right"
            :class="option.Length === Length.SHORT && 'option-active'"
            @click="option.Length = Length.SHORT"
          >
            Short
          </button>
        </div>
      </div>
      <button class="primary" @click="computeSlectedNames()">
        Generate Name
      </button>
    </div>

    <div class="cards-container">
      <div class="card" v-for="name in slected_names" :key="name">
        <h4>{{ name }}</h4>
        <p>x</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { Gender, Popularity, Length, names } from "@/data";

const slected_names = ref<string[]>([]);

interface OptionState {
  gender: Gender;
  popularity: Popularity;
  Length: Length;
}

const option = reactive<OptionState>({
  gender: Gender.BOY,
  popularity: Popularity.TRENDY,
  Length: Length.ALL,
});

const computeSlectedNames = () => {
  const filter_names = names
    .filter((name) => name.gender == option.gender)
    .filter((name) => name.popularity == option.popularity)
    .filter((name) => {
      if (option.Length === Length.ALL) return true;
      else return name.length == option.Length;
    });

  slected_names.value = filter_names.map((name) => name.name);
};
</script>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}
.options-container {
  background-color: rgb(250, 238, 202);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}
.option-container {
  margin-bottom: 2rem;
}
.option {
  background: white;
  outline: 0.3rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.7rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;

  font-weight: 200;
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
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}
.card p {
  position: absolute;
  top: -25%;
  left: 92.5%;
  cursor: pointer;
  color: rgb(225, 225, 225, 0.178);
}
</style>
