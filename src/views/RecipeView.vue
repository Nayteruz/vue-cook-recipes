<template>
  <div class="recipe">
    <router-link to="/">
      <button class="btn">&lt; Назад</button>
    </router-link>
    <h1>{{ recipe?.title }}</h1>
    <p class="desc">{{ recipe?.description }}</p>
    <div class="delimiter"></div>
    <div class="ingredients">
      <h3>Ингредиенты</h3>
      <ul>
        <li v-for="(ingredient, i) in recipe?.ingredients" :key="i+ingredient">
          {{ ingredient }}
        </li>
      </ul>
    </div>
    <div class="method">
      <h3>Способ приготовления</h3>
      <ol>
        <li v-for="(method, i) in recipe?.method" :key="method+i">
          <span v-html="cleanText(method)"></span>
        </li>
      </ol>
    </div>
  </div>
</template>

<script setup>
import {computed, onMounted} from "vue";
import {useStore} from "vuex";
import {useRoute} from 'vue-router';

const store = useStore();
const route = useRoute();

onMounted(() => {
  store.commit('LOAD_RECIPES');
})

const recipe = computed(() => store.state.recipes.find(recipe => recipe.slug === route.params.slug));

const cleanText = (text) => text.replace(/\n/g, '<br/>');
</script>

<style scoped lang="scss">
.recipe {
  padding: 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.desc {
  font-size: 1.125rem;
  line-height: 1.4;
  margin-bottom: 1rem;
}

.delimiter {
  margin-bottom: 1rem;
  background: rgba(#007bff, .7);
  height: 2px;
}

h3 {
  margin-bottom: 1rem;
}

.ingredients {
  padding: 1rem;
  background-color: #081c33;
  border-radius: 0.5rem;
  margin-bottom: 2rem;
  line-height: 1.2;


  ul {
    li {
      list-style-position: inside;
      line-height: 1.2;
      margin-bottom: 1rem;
    }
  }
}

.method {
  line-height: 1.2;

  ol {
    li {
      margin-bottom: 2rem;
      padding-bottom: 1rem;
      list-style-position: inside;
      border-bottom: 1px solid rgba(#007bff, .7);
    }
  }
}

.btn {
  margin-bottom: 10px;
}
</style>