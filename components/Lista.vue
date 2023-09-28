<template>
  <section>
    <div class="container-row">
      <div id="liste" class="container-wrap">
        <Character v-for="character in characters" :key="character.id" :character="character" />
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios';
import Character from '../components/Personaje';

export default {
  name: 'Lista',

  components: {
    Character,
  },

  data() {
    return {
      characters: [],
    };
  },

  beforeCreate() {
    axios.get(`http://gateway.marvel.com/v1/public/characters?ts=1&apikey=5bd987f4470c9f45b2dae9f51d1387db&hash=7c42b00f9898de246920fa7b29236598&limit=32`)
      .then((response) => {
        this.characters = response.data.data.results.filter(characters => {
          return !characters.thumbnail.path.includes("image_not_available");
        });
        console.log(response.data.data.results);
      });
  },

  methods: {
    actualizarLista(resultados) {
      this.characters = resultados;
    },
  },

  created() {
    this.$root.$on('resultadosBusqueda', this.actualizarLista);
  },

};
</script>

<style>
.container-row {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}

.container-wrap {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: flex-start;
}

#liste {
  width: 1050px;
  height: auto;
  margin: 40px;
}
</style>
