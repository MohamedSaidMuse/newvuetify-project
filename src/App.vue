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
      <div class="container">
    <Balance :total="23" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTransactionDeleted"
    />
    <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
  </div>
    </v-main>
  </v-app>
  
</template>
<style>
/* Ensure the parent of .container has full height */
html, body, #app, v-main {
  height: 100%;
  margin: 0;
}

/* Center .container vertically and horizontally */
.container {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Centers vertically */
  align-items: center; /* Centers horizontally */
  height: 100%;
}
</style>

<script setup>
  import { ref } from 'vue'
  import '@mdi/font/css/materialdesignicons.css'; // Ensure you import the MDI CSS
  
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
//import AddTransaction from './components/AddTransaction.vue';
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