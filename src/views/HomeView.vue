<template>
  <div class="home">
    <h1>Мои рецепты</h1>
    <button @click="togglePopup" class="btn btn-lg">Добавить рецепт</button>
    <div class="recipes">
      <CardItem
        :recipe="recipe"
        v-for="recipe in recipeListDesc"
        :key="recipe.slug"
        @removeRecipe="removeRecipe"
        @editRecipe="editRecipe"
      />
    </div>
    <div class="recipe-popup-wrap" v-if="popupOpen">
      <AddRecipe
        @togglePopup="togglePopup"
        @addNewRecipe="addNewRecipe"
        :oldRecipe="oldRecipe"
      />
    </div>
  </div>
</template>

<script>
import {ref, onMounted, computed} from 'vue'
import {useStore} from 'vuex'
import CardItem from "@/components/CardItem";
import AddRecipe from "@/components/AddRecipe";

export default {
  name: 'HomeView',
  components: {
    CardItem,
    AddRecipe
  },

  setup() {

    const oldRecipe = ref(null);

    const popupOpen = ref(false);
    const store = useStore();

    const togglePopup = () => {
      popupOpen.value = !popupOpen.value
      if(popupOpen.value === false){
        oldRecipe.value = {}
      }
    }

    const recipeListDesc = computed(() => {
      // eslint-disable-next-line vue/no-side-effects-in-computed-properties
      return store.state.recipes.sort((a, b) => {
        return b.createdAt - a.createdAt
      })
    });

    const addNewRecipe = (newRecipe) => {

      if (newRecipe.value.title === '') {
        alert('Необходимо ввести название!');
        return;
      }

      if(!oldRecipe.value?.slug){
        newRecipe.value.slug = newRecipe.value.title.toLowerCase().replace(/\s/g, '-') + '-' + Date.now().toString()
      }
      newRecipe.value.createdAt = Date.now();
      store.commit('ADD_RECIPE', {...newRecipe.value});

      if (oldRecipe.value) {
        store.commit('REMOVE_RECIPE', oldRecipe.value);
        oldRecipe.value = null;
      }

      togglePopup();
    }

    const removeRecipe = (recipe) => {
      store.commit('REMOVE_RECIPE', recipe);
    }

    const editRecipe = (recipe) => {
      oldRecipe.value = recipe;
      popupOpen.value = true;
    }

    onMounted(() => {
      store.commit('LOAD_RECIPES');
    })

    return {
      popupOpen,
      togglePopup,
      addNewRecipe,
      removeRecipe,
      oldRecipe,
      editRecipe,
      recipeListDesc
    }
  }
}
</script>

<style lang="scss">
.home {
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1 {
  font-size: 3rem;
  margin-bottom: 32px;
}

.recipes {
  margin-top: 1rem;
  width: 100%;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 15px;
  max-width: 1200px;

  @media all and (max-width:1024px) {
    grid-template-columns: repeat(2, 1fr);
  }
  @media all and (max-width:768px) {
    grid-template-columns: repeat(1, 1fr);
  }
}

.recipe-popup-wrap {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  overflow-y: auto;
  min-height: 0;
}

.add-recipe {
  font-size: 30px;
}


</style>


