<template>
  <div class="add-recipe-popup">
    <div class="popup-content">
      <button type="button" class="btn btn-danger close-pop" @click="togglePopup">×</button>
      <h2>{{ recipe?.title ? 'Редактировать рецепт' : 'Новый рецепт' }}</h2>
      <form @submit.prevent="addNewRecipe">
        <div class="group">
          <label>Название</label>
          <input type="text" v-model="recipe.title">
        </div>
        <div class="group">
          <label>Описание</label>
          <textarea v-model="recipe.description"></textarea>
        </div>
        <div class="group">
          <label>Ингредиенты</label>
          <div class="ingredient" v-for="i in recipe.ingredientRows" :key="i">
            <input type="text" v-model="recipe.ingredients[i - 1]">
          </div>
          <button type="button" @click="addNewIngredient" class="btn">Добавить ингредиент</button>
        </div>
        <div class="group">
          <label>Способ приготовления</label>
          <div class="methods" v-for="i in recipe.methodRows" :key="i">
            <textarea v-model="recipe.method[i - 1]"></textarea>
          </div>
          <button type="button" @click="addNewStep" class="btn">Добавить шаг</button>
        </div>
        <div class="buttons">
          <button type="submit" class="btn btn-primary btn-lg">
            {{ recipe?.title ? 'Редактировать рецепт' : 'Добавить рецепт' }}
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script setup="props">
import {defineEmits, defineProps, ref, toRefs} from 'vue'

const props = defineProps({
  oldRecipe: Object,
})
const {oldRecipe} = toRefs(props);

const emit = defineEmits(['togglePopup', 'addNewRecipe']);

const newRecipe = ref({
  title: '',
  description: '',
  ingredients: [],
  method: [],
  ingredientRows: 1,
  methodRows: 1
})

const recipe = ref(null);

if (oldRecipe.value?.title) {
  recipe.value = toRefs(oldRecipe.value)
} else {
  recipe.value = toRefs(newRecipe.value)
}

const addNewIngredient = () => {
    recipe.value.ingredientRows++;
}
const addNewStep = () => {
    recipe.value.methodRows++;
}

const togglePopup = () => emit('togglePopup')
const addNewRecipe = () => {
  emit('addNewRecipe', recipe);
  recipe.value = newRecipe.value;
}


</script>

<style scoped lang="scss">
.add-recipe-popup {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100%;
  margin: 10px;

  .popup-content {
    background-color: #081c33;
    padding: 2rem;
    border-radius: 1rem;
    width: 100%;
    max-width: 768px;
    position: relative;

    h2 {
      font-size: 2rem;
      margin-bottom: 1rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
    }

    .close-pop {
      position: absolute;
      right: 10px;
      top: 10px;
      font-weight: bold;
      font-size: 20px;
      padding: 0;
      line-height: 1;
      width: 30px;
      height: 30px;
    }

    .group {
      margin-bottom: 1rem;

      label {
        display: block;
        margin-bottom: 0.5rem;
      }

      input, textarea {
        display: block;
        width: 100%;
        padding: 0.5rem;
        border: 1px solid #ccc;
        border-radius: 5px;
        margin-bottom: 1rem;
        outline: none;
        font-size: 16px;
      }

      textarea {
        height: 100px;
        resize: none;
      }
    }
  }
}
</style>