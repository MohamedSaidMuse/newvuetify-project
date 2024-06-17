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
    <Balance :total="total" />
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
  font-size: 40px; /* Adjust font size as needed */
  color: #3498db; /* Example color: blue */
}
</style>

<script setup>
import { ref } from 'vue'
import '@mdi/font/css/materialdesignicons.css'; // Ensure you import the MDI CSS

import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';

import { computed, onMounted } from 'vue';

// Uncomment the next line if you need to use AddTransaction component
 import AddTransaction from './components/AddTransaction.vue';
 const transactions = ref([]);
// Reactive state using ref
const drawer = ref(null);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});
// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});
// Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});
// Submit transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount,
  });

  saveTransactionsToLocalStorage();

  //toast.success('Transaction added.');
};
// Generate unique ID
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );

  saveTransactionsToLocalStorage();

  //toast.success('Transaction deleted.');
};
// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
// Reactive array of items
const items = ref([
  { title: 'Home', icon: 'mdi-view-dashboard' },
  { title: 'Types', icon: 'mdi-help-box' },
  { title: 'Categories', icon: 'mdi-help-box' }, // Fixed typo in 'Categories'
]);
</script>
