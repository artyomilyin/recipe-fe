<template>
  <div class="p-5 rounded-xl max-w-sm mx-auto flex">
    <h1 class="text-3xl p-2 px-5 max-w-sm mx-auto">Recipe list</h1>
    <button @click="toggleAddForm"
            class="p-2 border rounded-xl max-w-sm ml-auto bg-green-100 ...">
      {{ showAddRecipe ? 'Close' : 'Add recipe' }}
    </button>
  </div>
  <div class="mx-10 p-5">
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
