<template>
  <div class="p-6 m-3 max-w-sm mx-auto rounded-xl shadow-lg bg-white">
    <div class="flex">
      <h3 class="text-2xl">{{ recipe.name }}</h3>
      <i @click="$emit('delete-recipe', recipe.id)"
         class="fa-sharp fa-solid fa-xmark m-2 ml-auto cursor-pointer"></i>
    </div>
    <p>Creator: {{ recipe.creator }}</p>
  </div>
</template>

<script>
export default {
  name: "Recipe",
  props: {
    recipe: Object
  }
}
</script>

<style scoped>
</style>
