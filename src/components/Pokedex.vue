<template>
  <div>
    <ListeTypesPokemon :pokemons="pokemons" />

    <label for="generation">Sélectionner une génération :</label>
    <select
      id="generation"
      v-model="selectedGeneration"
      @change="fetchPokemons"
    >
      <option value="all">Toutes les générations</option>
      <option
        v-for="generation in generations"
        :key="generation"
        :value="generation"
      >
        Génération {{ generation }}
      </option>
    </select>

    <label for="pokemonCount">Nombre de Pokémon :</label>
    <input
      type="number"
      id="pokemonCount"
      v-model="pokemonCount"
      @change="fetchPokemons"
    />

    <div class="pokemon-row">
      <Pokemon
        v-for="pokemon in pokemons"
        :key="pokemon.name"
        :pokemon="pokemon"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./Pokemon.vue";
import ListeTypesPokemon from "./ListeTypesPokemon.vue";
import DetailsPokemon from "./DetailsPokemon.vue";

export default {
  data() {
    return {
      pokemons: [],
      pokemonCount: 20,
      selectedGeneration: "all",
      generations: [],
    };
  },
  mounted() {
    this.fetchGenerations();
    this.fetchPokemons();
  },
  methods: {
    fetchGenerations() {
      const availableGenerations = [1, 2, 3, 4, 5, 6, 7, 8];
      this.generations = availableGenerations;
    },
    fetchPokemons() {
      if (this.pokemonCount > 0) {
        const apiUrl =
          this.selectedGeneration === "all"
            ? `https://pokebuildapi.fr/api/v1/pokemon/limit/${this.pokemonCount}`
            : `https://pokebuildapi.fr/api/v1/pokemon/generation/${this.selectedGeneration}`;
        axios
          .get(apiUrl)
          .then((response) => {
            this.pokemons = response.data;
          })
          .catch((error) => {
            console.error("Error fetching data:", error);
          });
      } else {
        console.error("Le nombre de Pokémon doit être supérieur à zéro.");
      }
    },
    fetchPokemonDetails(pokemonId) {
      const apiUrl = `https://pokebuildapi.fr/api/v1/pokemon/${pokemonId}`;
      axios
        .get(apiUrl)
        .then((response) => {})
        .catch((error) => {
          console.error("Error fetching Pokemon details:", error);
        });
    },
  },
  components: {
    Pokemon,
    ListeTypesPokemon,
    DetailsPokemon,
  },
  watch: {
    pokemonCount: function (newCount, oldCount) {
      if (newCount !== oldCount) {
        this.fetchPokemons();
      }
    },
    selectedGeneration: function (newGeneration, oldGeneration) {
      if (newGeneration !== oldGeneration) {
        this.fetchPokemons();
      }
    },
  },
};
</script>

<style scoped>
.type-counts {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
}

.type-item {
  display: flex;
  align-items: center;
  margin-right: 10px;
}

label {
  margin-right: 10px;
  margin-left: 40px;
  color: white;
  font-size: 20px;
}

.type-item img {
  width: 24px;
  height: 24px;
  margin-right: 4px;
}

.pokemon-row {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}
</style>