<script setup>
import { ref } from 'vue';


  const show = ref(false)
  const recipe = ref(null)
  const searchTerm = ref('')

  const post = () => {
            fetch('https://www.themealdb.com/api/json/v1/1/search.php?s='+searchTerm.value)
        .then((response) => response.json())
        .then((data) => {
          if(data.meals != null){
            recipe.value = data.meals[0]
            show.value = true
          }
          else
          show.value = false
        });
    }


</script>

<template>
<div>
    <input type="text" v-model="searchTerm" placeholder="search for a meal..." />
    <button @click="post">Search</button>
  </div>
   <div v-if="show">
    <h2>{{ recipe.strMeal }}</h2>
    <img :src="recipe.strMealThumb" />

    <p>
      {{ recipe.strInstructions }}
    </p>
  </div>
  <p v-else>Nothing found</p>
</template>

<style scoped>
div {
  margin-bottom: 20px;
}

input[type="text"] {
  padding: 10px;
  font-size: 16px;
  border: none;
  border-bottom: 1px solid #ccc;
  outline: none;
  transition: border-color 0.3s ease;
  margin-right: 1rem;
}

input[type="text"]:focus {
  border-color: #4CAF50;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

div[v-if="show"] {
  margin-top: 20px;
}

h2 {
  font-size: 24px;
  margin-bottom: 10px;
}

img {
  max-width: 100%;
  margin-bottom: 10px;
  border-radius: 4px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

p {
  font-size: 16px;
  line-height: 1.5;
}
</style>
