<template>
  <div class="type-list">
    <h1>Types de Pokémon</h1>

    <div v-for="(count, type) in typeCounts" :key="type" class="type-item">
      <div class="type-content">
        <img :src="getTypeImage(type)" alt="Type Image" />
        <span>{{ type }} : {{ count }}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    pokemons: Array,
  },
  computed: {
    typeCounts() {
      const counts = {};
      this.pokemons.forEach((pokemon) => {
        const primaryType = pokemon.apiTypes[0].name;
        counts[primaryType] = (counts[primaryType] || 0) + 1;
      });
      return counts;
    },
  },
  methods: {
    getTypeImage(type) {
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
      return typeImages[type] || "";
    },
  },
};
</script>

<style scoped>
span {
  color: white;
}

.type-list {
  margin-top: 20px;
  display: flex;
  flex-wrap: wrap;
  text-align: center;
  background-color: #4b4b4b;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
  margin-bottom: 25px;
}

.type-list h1 {
  width: 100%;
  margin-bottom: 20px;
  color: #333;
  font-size: 54px;
}

.type-item {
  margin-right: 10px;
  display: flex;
  align-items: center;
  background-color: #767676;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 10px;
  padding: 10px;
}

.type-item:hover {
  background-color: #8e8e8e;
}

.type-item img {
  width: 24px;
  height: 24px;
  margin-right: 4px;
}

.type-content {
  display: flex;
  align-items: center;
}

.type-count {
  margin-left: auto;
  font-weight: bold;
}
</style>