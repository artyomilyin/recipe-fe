<template>
<form @submit="addRecipe" class="bg-white shadow-md rounded px-8 pt-6 pb-8">
  <div class="mb-4">
    <label class="block text-gray-700 text-sm font-bold mb-2" for="name">Recipe name</label>
    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" v-model="name" type="text" id="name" name="name"><br>
  </div>
  <div class="mb-4">
    <label class="block text-gray-700 text-sm font-bold mb-2" for="creator">Creator</label>
    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" v-model="creator" type="text" id="creator" name="creator"><br>
  </div>
  <div class="mb-4">
    <button @click="addRecipe" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
      Save
    </button>
  </div>
</form>
</template>

<script>
export default {
  name: "AddRecipeForm",
  data() {
    return {
      name: '',
      creator: '',
    }
  },
  methods: {
    addRecipe (e) {
      e.preventDefault()
      if(!this.name) {
        alert('Fill in the recipe name.')
        return
      }
      const newRecipe = {
        id: Math.floor(Math.random() * 100000),
        name: this.name,
        creator: this.creator,
      }
      this.name = ''
      this.creator = ''
      this.$emit('add-recipe', newRecipe)
    }
  }
}
</script>

<style scoped>

</style>