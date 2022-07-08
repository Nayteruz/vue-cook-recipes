<template>
  <div class="card">
    <span @click="removeRecipe(recipe)" class="btn btn-danger">Удалить</span>
    <h2>{{ recipe.title.length > 25 ? recipe.title.slice(0, 25) + '...' : recipe.title }}</h2>
    <p>{{ recipe.description.length > 50 ? recipe.description.slice(0, 100) + '...' : recipe.description }}</p>
    <div class="buttons">
      <router-link :to="`recipe/${recipe.slug}`">
        <button class="btn btn-primary">Посмотреть</button>
      </router-link>
      <button @click="editRecipe(recipe)" class="btn btn-info">Редактировать</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CardItem',
  props: ['recipe']
}
</script>


<script setup>
import {defineEmits} from 'vue'

const emit = defineEmits(['removeRecipe', 'editRecipe'])

const removeRecipe = (recipe) => {
  emit('removeRecipe', recipe)
}

const editRecipe = (recipe) => {
  emit('editRecipe', recipe)
}

</script>

<style scoped lang="scss">
.card {
  padding: 1rem;
  border-radius: 5px;
  background-color: #081c33;
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 10px;

  span {
    margin-left: auto;
    padding: 2px 4px;
    font-size: 12px;
  }

  h2 {
    font-size: 20px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis;
  }

  p {
    font-size: 14px;
    line-height: 1.4;
  }

  .buttons {
    display: flex;
    align-items: center;
    justify-content: space-between;
    gap: 20px;
    margin-top: auto;
    button {
      font-size: 14px;
    }
  }
}
</style>