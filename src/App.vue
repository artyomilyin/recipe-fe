<template>
  <header>
    <div>
      <h1>Recipe list</h1>
    </div>
  </header>
  <div class="p-5 container">
    <button @click="toggleAddForm" class="p-5 border ...">
      {{ showAddRecipe ? 'Close' : 'Add recipe' }}
    </button>
    <div v-show="showAddRecipe">
      <AddRecipeForm @add-recipe="addRecipe"></AddRecipeForm>
    </div>
    <RecipeList @delete-recipe="deleteRecipe" :recipes="recipes"/>
  </div>
</template>

<script>
import RecipeList from './components/RecipeList.vue'
import AddRecipeForm from "./components/AddRecipeForm.vue";

export default {
  data() {
    return {
      recipes: [],
      showAddRecipe: false
    }
  },
  components: {AddRecipeForm, RecipeList},
  methods: {
    deleteRecipe(id) {
      this.recipes = this.recipes.filter((recipe) => recipe.id !== id)
    },
    addRecipe(newRecipe) {
      this.recipes = [...this.recipes, newRecipe]
    },
    toggleAddForm() {
      this.showAddRecipe = !this.showAddRecipe
    }
  },
  mounted() {
    this.recipes = [
      {id: 1, name: 'Name 1', creator: 'Me'},
      {id: 2, name: 'Recipe 2', creator: 'Somebody else'},
      {id: 3, name: 'My favourite chicken', creator: 'Raymond'},
    ]
  }
}
</script>

<style scoped>
</style>
