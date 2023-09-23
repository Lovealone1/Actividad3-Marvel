<template>
  <div>
    <div id="lignes" class="container-col">
      <div
        id="image"
        :style="{ backgroundImage: characterImageStyle }"
        @click="toggleCharacterData"
      ></div>
      <div id="nom" class="container-row">
        <h1 @click="toggleCharacterData">{{ character.name }}</h1>
      </div>
    </div>

    <div v-if="characterData" id="modal" class="modal-body">
      <div style="margin: 4px">
        <div>{{ character.description }}</div>
        <div style="height: 8px;"></div>

        <div style="color:black">
          <div>
            Comics: {{ character.comics.available }},
            Series: {{ character.series.available }}
          </div>
          <div>
            Historias: {{ character.stories.available }},
            Eventos: {{ character.events.available }}
          </div>
        </div>

        <div style="height: 8px;"></div>
        <div>SOME EVENT NAMES:</div>

        <div v-for="serie in characterSeries" :key="serie.name">
          {{ serie.name }}
        </div>

        <div style="height: 10px;"></div>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
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
}

.container-col {
  display: flex;
  flex-direction: column;
  margin: 6px;
}

#lignes {
  width: 250px;
  height: 300px;
  border-radius: 10px;
}

#lignes:hover {
  border: 2px solid #e92227;
}

#image {
  width: 100%;
  height: 100%;
  background-size: cover;
  border-radius: 10px 10px 0px 0px;
  border: 1px solid rgba(180, 180, 180, 0.781);
}

#nom {
  background-color: white;
  border: 1px solid rgba(180, 180, 180, 0.781);
  width: 100%;
  height: 80px;
  border-radius: 0px 0px 10px 10px;
}

h1 {
  font-size: 20px;
  height: auto;
  text-align: center;
  color: black;
}

h1:hover {
  font-size: 25px;
  color: #e92227;
}

#modalName {
  font-size: 25px;
  text-align: center;
  color: black;
  height: 80px;
}

#modal {
  width: 250px;
  height: auto;
  font-size: 15px;
  background-color: #f1f2f0;
  text-align: center;
  margin-bottom: 20px;
  margin-left: 6px;
  border-radius: 10px 10px 10px 10px;
}

button {
  height: auto;
  width: 100px;
  background-color: #4796ea;
  margin-bottom: 5px;
  align-content: center;
  text-decoration-color: white;
  border-radius: 8px;
}
</style>
