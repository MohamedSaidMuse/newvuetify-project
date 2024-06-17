<template>
    <div class="inc-exp-container">
      <div :class="{'small-screen': $mq === 'mobile'}">
        <h4>Income</h4>
        <p id="money-plus" class="money plus">+${{ income }}</p>
      </div>
      <div :class="{'small-screen': $mq === 'mobile'}">
        <h4>Expense</h4>
        <p id="money-minus" class="money minus">${{ expenses }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from 'vue';
  
  const props = defineProps({
    income: {
      type: Number,
      required: true,
    },
    expenses: {
      type: Number,
      required: true,
    },
  });
  </script>
  
  <style scoped>
  .small-screen h4, .small-screen .money {
    text-align: center;
  }
  
  /* You can also use media queries for additional responsiveness */
  @media (max-width: 768px) {
    .inc-exp-container {
      padding: 10px;
    }
  }
  </style>