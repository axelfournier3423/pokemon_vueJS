<template>
  <div
    :style="{ backgroundColor: getTypeColor(pokemon.apiTypes[0].name) }"
    class="pokemon-card"
  >
    <router-link :to="'/pokemon/' + pokemon.id">
      <div id="gen">
        <p>Génération {{ pokemon.apiGeneration }}</p>
      </div>
      <img class="pokimg" :src="pokemon.image" alt="Pokemon Image" />
      <h2>{{ pokemon.name }}</h2>

      <div class="types-container">
        <div v-for="type in pokemon.apiTypes" :key="type.name" class="type">
          <img class="typeimg" :src="type.image" :alt="type.name" />
        </div>
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getTypeColor(typeName) {
      console.log("Type Name:", typeName);
      const typeColors = {
        grass: "green",
        feu: "red",
        eau: "blue",
        insecte: "brown",
        vol: "lightblue",
        poison: "purple",
        normal: "gray",
        electrik: "yellow",
        sol: "brown",
        fee: "pink",
        combat: "red",
        psy: "pink",
        acier: "gray",
        roche: "brown",
        dragon: "purple",
        tenebres: "darkgray",
        spectre: "darkgray",
        glace: "lightblue",
      };

      const lowerCaseTypeName = typeName.toLowerCase();

      const backgroundColor = typeColors[lowerCaseTypeName] || "gray";

      return backgroundColor;
    },
  },
};
</script>

<style>
.pokemon-card {
  border: 1px solid #ccc;
  padding-bottom: 10px;
  margin-right: auto;
  margin-left: auto;
  margin-top: 20px;
  margin-bottom: 20px;
  width: 28%;
  border-radius: 45px;
  text-align: center;
}

#gen {
  margin-top: 0;
  border-bottom: 5px solid black;
  width: 100%;
}

#gen p {
  font-size: 150%;
}

.types-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;
}

.type {
  margin-right: 8px;
}

div h2 {
  margin-top: 5px;
  font-size: 300%;
  color: rgb(199, 197, 197);
}

.pokimg {
  width: 70%;
}

.typeimg {
  width: 50%;
}
</style>