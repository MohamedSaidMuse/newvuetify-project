<template>
  <v-app id="inspire">
    <v-navigation-drawer
    v-model="drawer"
    app
  
    >
  <v-list-item title="My Application" subtitle="Vuetify"></v-list-item>
  <v-divider></v-divider>
<v-list-item link>
  <v-list-item-icon>
    <v-icon>mdi-home</v-icon>
  </v-list-item-icon>
  <v-list-item-content>
    <v-list-item-title>Home</v-list-item-title>
  </v-list-item-content>
</v-list-item>
<v-list-item link>
  <v-list-item-icon>
    <v-icon>mdi-format-list-bulleted-type</v-icon>
  </v-list-item-icon>
  <v-list-item-content>
    <v-list-item-title>Types</v-list-item-title>
  </v-list-item-content>
</v-list-item>
<v-list-item link>
  <v-list-item-icon>
    <v-icon>mdi-view-list</v-icon>
  </v-list-item-icon>
  <v-list-item-content>
    <v-list-item-title>Categories</v-list-item-title>
  </v-list-item-content>
</v-list-item>
</v-navigation-drawer>
  

    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-app-bar-title>Application</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <!--  -->
    </v-main>
  </v-app>
</template>


<script setup>
  import { ref } from 'vue'
  import '@mdi/font/css/materialdesignicons.css'; // Ensure you import the MDI CSS

  const drawer = ref(null)
</script>

<script>
/*<!--<v-list-item link title="Home"></v-list-item>
  <v-list-item link title="Types"></v-list-item>
  <v-list-item link title="Categrories"></v-list-item>-->*/
  export default {
    data: () => ({ drawer: null,
  items: [
    {title:'Home'  , icon:'mdi-view-dashboard'},
    {title:'Types'  , icon:'mdi-help-box'},
    {title:'Categrories'  , icon:'mdi-help-box'},
    ],
     }),
  }
</script>