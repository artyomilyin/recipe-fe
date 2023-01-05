<template>
  <div class="p-6 m-3 max-w-sm mx-auto bg-white rounded-xl shadow-lg">
    <div>
      <i @click="$emit('delete-recipe', recipe.id)"
         class="fa-sharp fa-solid fa-xmark"></i>
    </div>
    <h3>{{ recipe.name }}</h3>
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