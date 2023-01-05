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
    async deleteRecipe(id) {
      const res = await fetch(`/api/recipes/${id}`, {
        method: 'DELETE'
      })
      await this.fetchRecipes()
    },
    async addRecipe(newRecipe) {
      const res = await fetch('/api/recipes', {
        method: 'POST',
        headers: {'Content-type': 'application/json'},
        body: JSON.stringify(newRecipe)})
      const savedRecipe = await res.json()
      this.recipes = [...this.recipes, savedRecipe]
    },
    toggleAddForm() {
      this.showAddRecipe = !this.showAddRecipe
    },
    async fetchRecipes() {
      const res = await fetch('/api/recipes')
      this.recipes = await res.json()
    }
  },
  async mounted() {
    await this.fetchRecipes()
  }
}
</script>

<style scoped>
</style>
