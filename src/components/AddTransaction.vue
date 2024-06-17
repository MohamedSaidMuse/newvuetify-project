<template class="container">
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="now"><div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" placeholder="Enter text..." v-model="text" />
    </div>
    <div class ="here">
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      ></div>
      <input
        type="text"
        id="amount"
        placeholder="Enter amount..."
        v-model="amount"
      />
    </div>
    <!-- Error message display -->
    <div v-if="errorMessage" class="error-message">{{ errorMessage }}</div>
    <button class="btn">Add transaction</button> </div>
  </form>


</template>
<style>
/* Ensure the parent of .container has full height */
html, body, #app, v-main {
  height: 100%;
  margin: 0;
}
.here {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Centers vertically */
  align-items: center; /* Centers horizontally */
  height: 100%;
  font-size: 25px; /* Adjust font size as needed */
  color: #3498db; /* Example color: blue */
}
.now {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Centers vertically */
  align-items: center; /* Centers horizontally */
  height: 100%;
  font-size: 25px; /* Adjust font size as needed */
  color: #3498db; /* Example color: blue */
}
/* Center .container vertically and horizontally */
.form-control {
  display: flex;
  flex-direction: column;
  justify-content: center; /* Centers vertically */
  align-items: center; /* Centers horizontally */
  height: 100%;
  font-size: 25px; /* Adjust font size as needed */
  color: #3498db; /* Example color: blue */
}
</style>
<script setup>
//import { useToast } from 'vue-toastification';
import { ref } from 'vue';

const text = ref('');
const amount = ref('');
const errorMessage = ref('');



// Get toast interface
//const toast = use();

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    errorMessage.value = 'Both fields must be filled'
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit('transactionSubmitted', transactionData);

  // Clear form fields
  text.value = '';
  amount.value = '';
};
</script>
