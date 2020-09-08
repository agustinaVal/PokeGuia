<template>
  <div>
    <nav>
      <img src="https://capitalgaming.mx/wp-content/uploads/2019/02/pok.jpg" class="poke" />
      <h1>Busca tus Pokemones</h1>
      <div class="PokeInput">
        <input v-model="nombre" type="text" @keyup.enter="buscarPokemon" />
        <button @click="buscarPokemon">Buscar</button>
      </div>
    </nav>
    <div class="bodyPoke">
      <div>
        <img :src="imagen" alt />
        <h2>{{ nombrePokemon }}</h2>
        <h6>
          <strong>movimientos</strong>
        </h6>
        <ul>
          <li v-for="(movimiento, i) in movimientos" :key="i">{{ movimiento.move.name }}</li>
        </ul>
        <h6>
          <strong>Habilidades</strong>
        </h6>
        <ul>
          <li v-for="(habilidad,i) in habilidades" :key="i">{{ habilidad.ability.name }}</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      nombre: "pikachu",
      pokemon: {
        name: "",
        sprites: { front_default: "" },
        moves: [],
        abilities: [],
      },
    };
  },
  created() {
    this.buscarPokemon();
  },
  methods: {
    buscarPokemon() {
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.nombre}`)
        .then(function (response) {
          return response.json();
        })
        .then((myJson) => {
          console.log(myJson);
          this.pokemon = myJson;
        });
    },
  },
  computed: {
    imagen() {
      return this.pokemon.sprites.front_default;
    },
    nombrePokemon() {
      return this.pokemon.name;
    },
    movimientos() {
      return this.pokemon.moves.slice(0, 10);
    },
    habilidades() {
      return this.pokemon.abilities;
    },
  },
};
</script>

<style scoped>
nav {
  width: 100%;
  height: auto;
  display: flex;
  justify-content: space-between;
  color: #e6bc2f;
  position: fixed;
  background-color: white;
}
.poke {
  width: 80px;
  height: 80px;
}

.PokeInput {
  padding: 30px;
  margin-right: 10px;
  border-radius: 5px;
}
.bodyPoke {
  padding-top: 100px;
  display: flex;
  justify-content: center;
  color: grey;
  font-family: serif;
}
h2 {
  color: black;
  font-size: 30px;
}
button {
  padding: 10px;
  color: coral;
  background-color: white;
}
input {
  padding: 10px;
}
</style>
