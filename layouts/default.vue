<template>
    <v-app>
      <v-card>
        <v-app-bar
          absolute
          dark
          height="200px"
          shrink-on-scroll
          src="https://i.imgur.com/bgR408Y.jpg">
  
        <template v-slot:extension>

        </template>
  
        </v-app-bar>
  
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
      }
    },
  }
  </script>
  
  <style>
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
  color: #ff4081; /* Color al pasar el ratón */
}

.footer-date {
  flex: 10;
  text-align: right;
}
  </style>