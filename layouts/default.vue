<template>
  <v-app>
    <v-card>
      <v-app-bar
        absolute
        dark
        height="200px"
        shrink-on-scroll
        src="https://i.imgur.com/bgR408Y.jpg"
      >
        <template v-slot:extension>
          <v-row justify="center">
            <v-col cols="8" md="4">
              <v-text-field
                v-model="searchQuery"
                label="Buscar personaje"
                placeholder="Ingrese el nombre del personaje"
                style="width: 68%; margin-left: 100px"
                append-icon="mdi-magnify"
                @click:append="searchCharacters"
              ></v-text-field>
            </v-col>
          </v-row>
        </template>
      </v-app-bar>
    </v-card>
    <v-card>
      <!-- Contenido adicional que desees agregar -->
    </v-card>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer>
      <div class="social-icons">
        <a href="https://web.facebook.com/dgsx999" target="_blank">
          <v-icon size="24">mdi-facebook</v-icon>
        </a>
        <a href="https://twitter.com/offdan_g" target="_blank">
          <v-icon size="24">mdi-twitter</v-icon>
        </a>
        <a href="https://www.instagram.com/offdan_g/" target="_blank">
          <v-icon size="24">mdi-instagram</v-icon>
        </a>
      </div>
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data() {
    return {
      title: 'MARVEL',
      searchQuery: '',
    };
  },
  methods: {
    async searchCharacters() {
      // Verificar que haya al menos 4 caracteres antes de realizar la búsqueda
      if (this.searchQuery.length < 4) {
        console.log('Ingrese al menos 4 caracteres para buscar.');
        return;
      }

      try {
        // Realiza la petición a la API de Marvel con el término de búsqueda
        const response = await fetch(`http://gateway.marvel.com/v1/public/characters?nameStartsWith=${this.searchQuery}&ts=1&apikey=5bd987f4470c9f45b2dae9f51d1387db&hash=7c42b00f9898de246920fa7b29236598`);

        // Verifica si la petición fue exitosa (código de respuesta 200)
        if (response.ok) {
          const data = await response.json();
          console.log('Personajes encontrados:', data.data.results);
          this.$root.$emit('resultadosBusqueda', data.data.results);
          // Aquí puedes manejar la respuesta y cargar los personajes encontrados
          // por ejemplo, actualizar una lista de personajes en tu componente
        } else {
          console.error('Error al buscar personajes:', response.statusText);
        }
      } catch (error) {
        console.error('Error en la búsqueda:', error);
      }
    }
  }
};
</script>

<style>
/* Estilos existentes ... */
.social-icons {
  display: flex;
  align-items: center;
}

.social-icons a {
  margin: 0 8px;
  color: #fff;
  text-decoration: none;
}

.social-icons a:hover {
  color: #ff4081;
}

.footer-date {
  flex: 10;
  text-align: right;
}

.search-btn {
  margin-left: 230px; /* Ajusta el margen izquierdo según sea necesario */
}
</style>
