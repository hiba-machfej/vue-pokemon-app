<template>
  <div class="about">
    <div
      v-if="pokemon"
      class="w-3/12 m-auto bg-purple-100 mt-4 shadow-2xl flex justify-center flex-col items-center"
    >
      <router-link
        class="flex p-4 justify-center text-4xl text-yellow-700 self-end"
        to="/"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M6 18L18 6M6 6l12 12"
          /></svg
      ></router-link>

      <h3 class="text-2xl text-green-900 uppercase">{{ pokemon.name }}</h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_shiny" />
        <img class="w-48" :src="pokemon.sprites.back_shiny" />
      </div>

      <h3 class="text-yellow-400">Types</h3>
      <div
        v-for="(type, idx) in pokemon.types"
        :key="idx"
        class="text-blue-900"
      >
        {{ type.type.name }}
      </div>
    </div>
  </div>
</template>
<script>
import { useRoute } from "vue-router";
import { reactive, toRefs } from "vue";

export default {
  setup() {
    const route = useRoute();

    const state = reactive({
      pokemon: null,
    });

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((response) => response.json())
      .then((data) => {
        state.pokemon = data;
      });
    return { ...toRefs(state) };
  },
};
</script>
