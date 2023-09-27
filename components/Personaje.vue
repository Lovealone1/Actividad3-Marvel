<template>
  <div>
    <div v-if="characterHasInfo" id="lignes" class="container-col">
      <div id="nom" class="container-row">
        <h1 @click="toggleCharacterData">{{ character.name }}</h1>
      </div>
      <div
        id="image"
        :style="{ backgroundImage: 'url(' + character.thumbnail.path + '.' + character.thumbnail.extension + ')' }"
        @click="toggleCharacterData"
      ></div>
    </div>

    <v-card v-if="characterData" class="character-card">
      <v-card-title>

      </v-card-title>
      <v-card-actions class="d-flex align-center justify-center"> 
        <v-btn color="grey" dark class="text-white" @click="dialog = true">Mostrar descripción</v-btn>
      </v-card-actions>
      <v-card-text>
        <div>
          <b>Comics:</b> {{ character.comics.available }},
          <b>Series:</b> {{ character.series.available }}
        </div>
        <div>
          <b>Historias:</b> {{ character.stories.available }},
          <b>Eventos:</b> {{ character.events.available }}
        </div>

        <div class="info-row">
          <b>Otras participaciones:</b>
          <ul>
            <li v-for="serie in characterSeries" :key="serie.name">{{ serie.name }}</li>
          </ul>
        </div>
      </v-card-text>

      <v-dialog v-model="dialog" max-width="500px">
        <v-card>
          <v-card-title class="headline">

          </v-card-title>
        <v-card-text>
          <p>{{ character.description }}</p>
        </v-card-text>
      </v-card>
    </v-dialog>
      
    </v-card>
  </div>
</template>

<script>
export default {
  name: "Personaje",
  props: {
    character: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      characterData: false,
      dialog: false, 
    };
  },
  computed: {
    characterImageStyle() {
      return {
        backgroundImage: `url(${this.character.thumbnail.path}.${this.character.thumbnail.extension})`,
      };
    },
    characterSeries() {
      return this.character.series.items.slice(0, 3);
    },
    containerColStyle() {
    return {
      boxShadow: '0 2px 4px rgba(0, 0, 0, 0.1)',
    };
  },
  containerRowStyle() {
    return {
      boxShadow: '0 2px 4px rgba(0, 0, 0, 0.1)',
    };
  },
  characterHasInfo() {
      return (
        this.character.comics.available > 0 ||
        this.character.series.available > 0 ||
        this.character.stories.available > 0 ||
        this.character.events.available > 0
      );
    },
},
  methods: {
    toggleCharacterData() {
      this.characterData = !this.characterData;
    },
  },
};
</script>

<style scoped>
.container-row {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.container-col {
  display: flex;
  flex-direction: column;
  margin: 5px;
}

#lignes {
  width: 250px;
  height: 300px;
  border-radius: 0px;
}

#lignes:hover {
  border: 2px solid #525252;
}

#image {
  width: 100%;
  height: 100%;
  background-size: cover;
  border-radius: 0px 0px 0px 0px;
  border: 1px solid rgba(180, 180, 180, 0.781);
}

#nom {
  background-color: white;
  border: 1px solid rgba(180, 180, 180, 0.781);
  width: 100%;
  height: 80px;
  border-radius: 0px 0px 0px 0px;
}

h1 {
  font-size: 20px;
  height: auto;
  text-align: center;
  color: black;
}

h1:hover {
  font-size: 25px;
  color: #000000;
}

.character-card {
  max-width: 250px; 
  margin: 20px auto; 
}

.info-row ul {
  list-style: none;
  padding: 0;
}

.character-info {
  padding: 16px; 
}

.character-info div, .character-info ul {
  margin-bottom: 8px; 
}
</style>