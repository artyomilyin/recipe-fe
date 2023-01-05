<template>
  <div :key="recipe.id" v-for="recipe in recipes">
    <Recipe @delete-recipe="$emit('delete-recipe', recipe.id)" :recipe="recipe"/>
  </div>
</template>

<script>
import Recipe from "./Recipe.vue";

export default {
  name: "RecipeList",
  components: {Recipe},
  props: {
    recipes: Array
  },
  emits: ['delete-recipe']
}
</script>

<style scoped>

</style>