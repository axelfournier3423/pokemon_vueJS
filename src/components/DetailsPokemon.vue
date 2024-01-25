<template>
  <div>
    <div :class="getTypeClass(pokemonData.apiTypes[0].name)" id="card">
      <h1>{{ pokemonData.name }}</h1>
      <div class="generation">Gén {{ pokemonData.apiGeneration }}</div>
      <div class="type-images">
        <img id="pokimage" :src="pokemonData.image" :alt="pokemonData.name" />
        <div class="types">
          <div
            class="type-image"
            v-for="type in pokemonData.apiTypes"
            :key="type.name"
          >
            <img
              :src="getTypeImageUrl(type.name)"
              :alt="type.name"
              title="type.name"
            />
          </div>
        </div>
      </div>
      <div class="hp">{{ pokemonData.stats.HP }} HP</div>
      <p>Attaque: {{ pokemonData.stats.attack }}</p>
      <p>Défense: {{ pokemonData.stats.defense }}</p>
      <p>Attaque Spéciale: {{ pokemonData.stats.special_attack }}</p>
      <p>Défense Spéciale: {{ pokemonData.stats.special_defense }}</p>
      <p>Vitesse: {{ pokemonData.stats.speed }}</p>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
      pokemonData: {},
    };
  },
  created() {
    const idPokemon = this.$route.params.id;

    const apiUrl = `https://pokebuildapi.fr/api/v1/pokemon/${idPokemon}`;

    axios
      .get(apiUrl)
      .then((response) => {
        this.pokemonData = response.data;
      })
      .catch((error) => {
        console.error(
          "Erreur lors de la récupération des données du Pokémon :",
          error
        );
      });
  },
  methods: {
    getTypeImageUrl(typeName) {
      const typeImages = {
        Plante:
          "https://static.wikia.nocookie.net/pokemongo/images/c/c5/Grass.png",
        Feu: "https://static.wikia.nocookie.net/pokemongo/images/3/30/Fire.png",
        Eau: "https://static.wikia.nocookie.net/pokemongo/images/9/9d/Water.png",
        Insecte:
          "https://static.wikia.nocookie.net/pokemongo/images/7/7d/Bug.png",
        Vol: "https://static.wikia.nocookie.net/pokemongo/images/7/7f/Flying.png",
        Normal:
          "https://static.wikia.nocookie.net/pokemongo/images/f/fb/Normal.png",
        Poison:
          "https://static.wikia.nocookie.net/pokemongo/images/0/05/Poison.png",
        Électrik:
          "https://static.wikia.nocookie.net/pokemongo/images/2/2f/Electric.png",
        Sol: "https://static.wikia.nocookie.net/pokemongo/images/8/8f/Ground.png",
        Fée: "https://static.wikia.nocookie.net/pokemongo/images/4/43/Fairy.png",
        Combat:
          "https://static.wikia.nocookie.net/pokemongo/images/3/30/Fighting.png",
        Psy: "https://static.wikia.nocookie.net/pokemongo/images/2/21/Psychic.png",
        Acier:
          "https://static.wikia.nocookie.net/pokemongo/images/c/c9/Steel.png",
        Roche:
          "https://static.wikia.nocookie.net/pokemongo/images/0/0b/Rock.png",
        Dragon:
          "https://static.wikia.nocookie.net/pokemongo/images/c/c7/Dragon.png",
        Ténèbres:
          "https://static.wikia.nocookie.net/pokemongo/images/0/0e/Dark.png",
        Spectre:
          "https://static.wikia.nocookie.net/pokemongo/images/a/ab/Ghost.png",
        Glace:
          "https://static.wikia.nocookie.net/pokemongo/images/7/77/Ice.png",
      };

      return typeImages[typeName] || "";
    },
    getTypeClass(typeName) {
      const typeClasses = {
        Plante: "bg-grass",
        Feu: "bg-fire",
        Eau: "bg-water",
        Insecte: "bg-bug",
        Vol: "bg-flying",
        Normal: "bg-normal",
        Poison: "bg-poison",
        Électrik: "bg-electric",
        Sol: "bg-ground",
        Fée: "bg-fairy",
        Combat: "bg-fighting",
        Psy: "bg-psychic",
        Acier: "bg-steel",
        Roche: "bg-rock",
        Dragon: "bg-dragon",
        Ténèbres: "bg-dark",
        Spectre: "bg-ghost",
        Glace: "bg-ice",
      };

      return typeClasses[typeName] || "bg-gray";
    },
  },
};
</script>

<style>
.bg-grass {
  background: green;
}

.bg-fire {
  background: red;
}

.bg-water {
  background: blue;
}

.bg-bug {
  background: brown;
}

.bg-flying {
  background: lightblue;
}

.bg-poison {
  background: purple;
}

.bg-normal {
  background: gray;
}

.bg-electric {
  background: yellow;
}

.bg-ground {
  background: brown;
}

.bg-fairy {
  background: pink;
}

.bg-fighting {
  background: red;
}

.bg-psychic {
  background: pink;
}

.bg-steel {
  background: gray;
}

.bg-rock {
  background: brown;
}

.bg-dragon {
  background: purple;
}

.bg-dark {
  background: darkgray;
}

.bg-ghost {
  background: darkgray;
}

.bg-ice {
  background: lightblue;
}
#card {
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  width: 100%;
  margin: 20px auto;
  padding: 20px;
  font-family: "Arial", sans-serif;
  position: relative;
}

.hp {
  color: #ffffff;
  font-size: 25px;
  position: absolute;
  top: 10px;
  right: 10px;
  background: #4a4442;
  padding: 3px 6px;
  border-radius: 3px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.4);
}

h1 {
  color: black;
  font-size: 1.5em;
  margin-bottom: 10px;
  text-align: center;
}

h1:hover {
  color: #858281;
}

#card:hover {
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.2);
}

img {
  width: 100%;
  height: auto;
}

#pokimage {
  border-bottom: 10px solid #222221;
}

.type-images {
  text-align: center;
  margin-bottom: 10px;
}

.type-image img {
  width: 60%;
}

.types {
  display: flex;
  justify-content: center;
  margin-top: 10px;
  border-bottom: 10px solid #222221;
}

.type-image {
  margin-right: 5px;
}

p {
  color: black;
  font-size: 20px;
  font-weight: bold;
  line-height: 1.5;
  padding-bottom: 10px;
}

p:hover {
  color: #333232;
}

.generation {
  position: absolute;
  top: 10px;
  left: 10px;
  font-size: 25px;
  background: #4a4442;
  color: #ffffff;
  padding: 3px 6px;
  border-radius: 3px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.4);
}

.generation:hover {
  background-color: #858281;
  color: white;
}

.hp:hover {
  background-color: #858281;
  color: white;
}
</style>